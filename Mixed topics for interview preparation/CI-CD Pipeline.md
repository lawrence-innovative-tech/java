#### **Purpose
- **CI (Continue Integration) -** Continue integration workflow checks every changes or pushes it will checks entire application unit and integration test and builds application. And Most of the exception identified here itself.
- **CD (Continue Deployment) -** The integration are completely tested, builds it automates deploy in production.
	1. GitHub actions
	2. Jenkins
	3. GitLab
- Ci-CD pipeline is event driven design, when code push repository ci/cd pipeline get triggers, run unit and integration test, if test has failed reports to particular developer.
- Success testing take build and deploy to staging to test application.
- If remove ci/cd 
#### **Top companies code maintenance
-  There are three type of maintenance
	1. Current or Working branch
	2. Release Branch
	3. Production Setup (Master or Main)
1. Current or Working branch - Clone master code or setup to new branch, once complete our code runs push into GitHub it's started ci(test, build, create PR to if testing exist).
2. Release Branch - Once passes all the testing code moves to Release branch to production deployment.
3. Production branch - After deployment monitors few days on production. Then merge to master or main.

#### **Sample script with Explanation
``` java
name: Microservice Pipeline

on:
  push: 
    branches: ["features/*"]
  pull_request: 
    branches: ["main"]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
      - name: Set up java
        uses: actions/setup-java@v4
        with: 
          java-version: '17'
          distribution: 'temurin'
      - name: Java build maven
        run: mvn clean install
        
        
Optimized

name: Java CI & Release Pipeline   # Better, clear name

/*# ====================== TRIGGERS ====================== */
on:
  push:
    branches: 
      - "main"           # Final checks on main
      - "features/**"    # Runs on every feature branch push (your style)
  pull_request:
    branches: [ "main" ] # Runs when PR is created/updated to main
  push:
    tags: [ 'v*' ]       # Automatically triggers Release when you push tag (v1.2.3)

/* # ====================== PERMISSIONS ====================== */
permissions:
  contents: write          # Required for creating releases
  checks: write            # For nice test reports in PR

jobs:

/*  # ====================== BUILD & TEST JOB ====================== */
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'
          cache: maven                    # ← Huge speed improvement (caches dependencies)

      - name: Build & Run Tests
        run: mvn clean verify -B --no-transfer-progress   # Better than "clean install"

      - name: Upload Test Report (JUnit)
        uses: actions/upload-artifact@v4
        if: always()                       # Upload even if tests fail
        with:
          name: test-reports
          path: target/surefire-reports//*.xml

      - name: Upload Built JAR
        uses: actions/upload-artifact@v4
        with:
          name: app-jar
          path: target//*.jar
          retention-days: 7

  /*# ====================== RELEASE JOB (Only when you create tag) ======================*/
  release:
    needs: build                        # Wait for build to succeed
    if: startsWith(github.ref, 'refs/tags/')   # Runs only on tags like v1.0.0
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4
        with:
          fetch-depth: 0                # Get all history for changelog

      - name: Download JAR
        uses: actions/download-artifact@v4
        with:
          name: app-jar
          path: target

      - name: Create GitHub Release
        uses: softprops/action-gh-release@v2
        with:
          files: target//*.jar
          generate_release_notes: true     # Auto creates beautiful changelog
          draft: false
          prerelease: false
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

Deployment
```YAML
name: Java CI/CD + Docker + Sonar + Deploy

on:
  push:
    branches: [ "main", "features/**" ]
    tags: [ 'v*' ]
  pull_request:
    branches: [ "main" ]

permissions:
  contents: write
  checks: write
  pull-requests: write

jobs:
  build-and-analyze:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'
          cache: maven

      - name: Build + Test + JaCoCo Coverage
        run: mvn clean verify -B --no-transfer-progress

      - name: SonarCloud Analysis
        env:
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
          SONAR_HOST_URL: https://sonarcloud.io
        run: mvn sonar:sonar -Dsonar.projectKey=YOUR_PROJECT_KEY -Dsonar.organization=YOUR_ORG_KEY -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.login=$SONAR_TOKEN

      - name: Publish Coverage Report to PR
        uses: madrapps/jacoco-report@v1.7.0
        with:
          paths: target/site/jacoco/jacoco.xml
          token: ${{ secrets.GITHUB_TOKEN }}
          min-coverage-overall: 70
          update-comment: true

      - name: Upload Coverage HTML Report
        uses: actions/upload-artifact@v4
        with:
          name: code-coverage
          path: target/site/jacoco

  # ====================== DOCKER + DEPLOY (Only on Release Tag) ======================
  docker-and-deploy:
    needs: build-and-analyze
    if: startsWith(github.ref, 'refs/tags/v')
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Set up JDK 17 (for Maven)
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Build JAR
        run: mvn clean package -DskipTests

      - name: Login to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Login to GHCR
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Build & Push Docker Image
        uses: docker/build-push-action@v6
        with:
          context: .
          push: true
          tags: |
            ghcr.io/${{ github.repository }}:${{ github.ref_name }}
            ghcr.io/${{ github.repository }}:latest
            ${{ secrets.DOCKERHUB_USERNAME }}/microservice:${{ github.ref_name }}
            ${{ secrets.DOCKERHUB_USERNAME }}/microservice:latest
          platforms: linux/amd64

      - name: Deploy to Render
        run: curl -X POST ${{ secrets.RENDER_DEPLOY_HOOK }}
```

Artifact is equal to .jar or produce any file or folder in pipeline.