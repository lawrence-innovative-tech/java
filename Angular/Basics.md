#### **Angular Lifecycle
- Constructor - When Typescript component calls, it invoke constructor, Constructor inject dependencies.
- ngOnChanges - it detect changes on element and give to ts.
- ngOnInit - initialized necessary thinks to be here, external api, and internal process. Reactive programming invoke this to preform.
- ngDoCheck - Detact after update form, if there any changes or there.
- ngAfterContentInit - Initliazing content of that components.
- ngAfterContectInitCheck 

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
- 