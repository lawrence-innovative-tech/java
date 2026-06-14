
#### **Component
- Component handles user interface. The view part. It holds HTML, CSS part of the angular project.
- After Angular 14+ it handles one more condition for standalone. If, Component define as standalone it holds all the necessary to that angular.
- **The route initiate to component class after component creates instance for that class it start to initiate to load DOM with help of Component decorator.**
#### **Directives
- Directive is class is help change behaviour of HTML element or change appearance of DOM.
- Ex, ngIf, ngFor, ngClass (for style changes appearance).
#### **Decorators
- Extensive provide metadata to classes, methods, properties and parameter.
- In simple term, It like java annotations.
	- ex, 
		1. @Component
		2. @NgModules
		3. @ViewChild or or @ViewChildren
		4. @ContentChild or @ContentChildren
		5. @HostBiner or @HostListener

#### **Angular Lifecycle
- Constructor - When Typescript component calls, it invoke constructor, Constructor inject dependencies.
- ngOnChanges - it detect changes @Input values from parent, instantly fires child component child detect and made changes using Simple Changes.
- ngOnInit - run only once, after ngOnChanges, initialized necessary thinks to be here, external api, and internal process. Reactive programming invoke this to preform.
- ngDoCheck - Detect after update form, if there any changes or there.
- ngAfterContentInit - The has content child has use that parent content.
- ngAfterContectChecked - After content initialling it detect changes and updates.
- ngAfterViewInit - It fully responsible for child content the own content. it emit output to parent usages.
- ngAfterViewChecked - After changes it will detect and updates.
- ngOnDestory - unsubcribed, setTimeOut, setTimeInterval async process may guide to memory leak. Destoty wait untill it exist or clear.

#### **Directives
- Made changes on existing DOM elements or components.
- Directives won't have templates. It uses Dom elements.
- There are three components are there
	1. Components - it has own template UI + Data.
	2. Structural - Control particular changes are needs to update or not 
	3. Attribute - Control element and property in DOM.
#### **Data Binding
- Data combined and work with UI and Typescript class.
- There four data binding,
	1. Interpolation {{ }} - One way binding with HTML text content.
	2. Property binding [ ] - ts to html element to property binding.
	3. Event () - One way binding, bind to ts with user event mouse, click. key press-up.
	4. Two way binding [( )] - Property + Event binding communication two way.
#### Template-driven VS Reactive Forms
- Template driven form use directive use angular controls and maintain formgroup and form controls.
- Its asynchronous process. It use ngmodel two way binds.
- We declare in Html itself.
- Reactive form control and declarative in typescript so we needs to control formgroup and form controls. 
- Its synchronous process. Easy handle complex form and dynamic forms.
- Reactive form is one bind using formcontrolname.

#### **Promise
- Process asynchronous process eventual completion or failure. It returns resulting of the value.
- it contains, then(), catch(), finally() methods.

#### **Observable
- Process asynchronous streams of data emit multiple values over time. It an lazy when subscribe the observable it start to execution. It allow to process RxJS.

#### **Routing
- Routing is mechanism navigation between page or view in single page application without reloading page. 
- It map url to specific component that handles rendering and appropriate content dynamically.
- In modern way use **providerRouter(routes)** in **main.ts or app.config** file.
- **Standalone Component** is self contained it necessary imports, directive, decorator and it helps to achieve lazy loading also. It not belongs to retain in module based architecture.

```typescript

// Route config
import { Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';

export const routes: Routes = [
  { path: '', component: HomeComponent },           // default route
  { path: 'about', component: AboutComponent },
  { path: 'dashboard', loadComponent: () => import('./dashboard/dashboard.component').then(m => m.DashboardComponent) }, // lazy loading
  { path: '**', redirectTo: '' }                    // wildcard (404)
];

// app.config.ts or main.ts
import { provideRouter } from '@angular/router';
import { routes } from './app.routes';

bootstrapApplication(AppComponent, {
  providers: [provideRouter(routes)]
});

//Standalone component
import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { RouterOutlet } from '@angular/router';

@Component({
  selector: 'app-root',
  standalone: true,          // ← This makes it standalone
  imports: [CommonModule, RouterOutlet],  // ← Direct imports
  templateUrl: './app.component.html'
})
export class AppComponent { }
```

#### **Auth guard or Router guard
- It control navigation, only get access authenticated user and user has permission. 
- It's protects the routes, Only authenticated user can perform other access.
- Types,
	1. canActivate - Check active route have access to user
	2. canActivateChild - It active route's child route get access or not 
	3. canDeactivate - Before destroy component check unsaved form ?
	4. canMatch - can match is role based, but need to verify.
