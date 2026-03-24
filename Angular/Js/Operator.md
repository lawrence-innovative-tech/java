#### **Spread operator
- Spread object copies or merge the array elements. array allows duplicate because it's index based.
- Spread or expands array fields into individual values. This called Array Thread operator.
- Final, it return single array or object.
``` java
this.showCheckboxes = true;
this.columns = ['id', 'name']

ngAfterViewInit() {  
  this.displayedColumns = [  
    ...(this.showCheckboxes ? ['select'] : []),  
    ...this.columns.map(c=> c.columnDef)];  
  this.updateDataSource();  
}

Output:
['select', 'id', 'name']
```

- **Object Operator -** if object has key and value if same key occurs overrides same key values.
```java

const defaults = { theme: 'light', language: 'en', currency: 'INR' };
const userSettings = { theme: 'dark', city: 'Chennai' };

const finalSettings = { ...defaults, ...userSettings };

console.log(finalSettings);
// Output: { theme: 'dark', language: 'en', currency: 'INR', city: 'Chennai' }
```

#### **Rest Operator
- Opposite of spread operator, It used to split array or object value and stores individual variables.
- Handling duplication same as spread operator.
```java
// For Array
const fruits = ['apple', 'banana', 'apple', 'mango', 'apple'];

const [firstFruit, ...remainingFruits] = fruits;

console.log(remainingFruits); 
// Output: ['banana', 'apple', 'mango', 'apple']  ← duplicates kept

// For Object
const user = {
  name: 'Thiva',
  age: 25,
  city: 'Chennai',
  role: 'User',
  age: 30          // ← this would overwrite the previous 'age'
};

const { name, ...restInfo } = user;

console.log(restInfo);
// Output: { age: 30, city: 'Chennai', role: 'User' }   ← no duplicates possible
```