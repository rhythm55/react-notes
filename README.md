# react-notes

### Q: Difference between library and framework

A: 
- Library:
  - A collection of functions/classes that you can call to perform specific action
  - You remain in control of the flow of the application and choose when to call library
- Framework:
  - Provides a skeleton where application code is plugged in
  - It dictates the flow of control   
- The main differene is in a library you call the code and in framework code calls you
- Framework provides structure for building the application while libraries are more flexible

***

### Q: What is CDN . Why do we use it

A: 
- CDN stands for content delivery network
- it is a network of distributed systems that work together to deliver content to user based on geographical location.
- reduces latency(delay between the sender and receiver in a communication network) 
  and improve the performance of loading web page.

Why to use
- Faster Content delivery: By caching content on servers located near you - reduces latency
- Scalability: CDN can handle large amount of traffic and distriubte it accross their network of servers i.e less load on origin server
- Reliability: CDNs offer redundancy and failover mechanisms, ensuring that content is always available even if some servers fail.
- Cost-Effectiveness: CDNs can help reduce bandwidth costs by offloading traffic from origin servers and optimizing content delivery.

***

### Q: What is Config Driven UI?

A:
- design approach where the user interface of an application is largely 
defined and controlled by configuration rather than hard-coded logic

- In a config-driven UI, various aspects of the UI, 
such as layout, styling, and behavior, are specified in configuration 
files or data structures that can be easily modified without changing the underlying code.

***

### Q: What is the difference bw `dependency` and ` devDependencies`

A: 

- devDependencies
    - used in development phase only
    ex: Parcel
    ```
    npm install -D parcel
    ```

- dependency:
    - used in production phase 
    ex: React
    ```
    npm install react
    ```

***

### Q: ^ and ~ in pacakge.json

A:

 - `^` if there is a minor upgrade - next time we do npm i - automatically minor verison will be upgraded
        ex: `^2.3.4^` and new version `2.3.5` is released then it will be installed automatically
- `~` automatically installas major verison
         ex: `^2.3.4^` and new version `4.3.5` is released then it will be installed automatically

***

### React Fiber

- React Fiber is a concept of ReactJS that is used to render a system faster, smoother and smarter.
- became the default reconciler for React 16 and above
- Fiber is a plain js object with some properties. Represents a unit of work (ex. work is state change, changes in DOM)
- Fiber is asynchronous, React can:
    - Split work into chunks and prioritize tasks
    - Pause, resume, and restart rendering work on components as new updates come in
    - Reuse previously completed work and even abort it if not needed
***

# React Fiber Reconciliation
-process of syncing virtual DOM with actual DOM
- When we make changes or add data, React creates a new Virtual DOM and compares it with the previous one. Comparison is done by `Diffing Algorithm`. 
- Diff algorithm: Finds out the diff between old virtual DOM and new virtual DOM
- note: Finding out diff between two js objects is fast as compared to diff between actual DOMs
- It finds out the changed nodes and updates only the changed nodes in Real DOM leaving the rest nodes as it is. This process is called Reconciliation.
- Diffing algo assumptions -
    1. two elements in same position but in different type - react will re render the node and old component will unmount
        ```
          // old
          <div><h1>Title</h1></div>

          //new
          <div><h2>Title</h2></div>
        ```
    2. two elements same type and element but different attribute - react will keep same underline DOM and only update the attributes that got changed
        ```
        // only className will be changed
           // old
          <div className="before">some</div>

          //new
          <div className="after">some</div>
        ```
    3. Component update - keeps the same instace just updates the props passed to it i.e update props and render
        ```
        // only className will be changed
           // old
          <Welcome name="first"/>

          //new
          <Welcome name="last"/>
        ```
        
    4. Children : compare and render : consider a li elements - where a new li inserted at first place - now rest of the elements are same just becuase one new element inserted at top it should not re render whole list - it will be inefficient. In order to make it efficient react uses `key` to compare . by comparing key it can know which one are just reshuffled and doesnt need re rendering and which one needs to be rendered.
       ```
        // only li with key 4 will re rendered 
           // old
          <ul>
            <li key={1}>1</li>
            <li key={2}>2</li>
          </ul>

          //new
           <ul>
            <li key={4}>4</li>
            <li key={1}>1</li>
            <li key={2}>2</li>
          </ul>
        ```

***

### Q: Diff bw react and reactDOM

A: 
- React:
    - it is the core library for building user interface
    - provides the main API for defining React components like createComponent

- ReactDOM:
    - It is the library that provides DOM-specific methods for rendering React components.
    - ReactDOM is specific to web development

***


### Create Element
- `React.createElement`
- it creates a React Element which is js object
- accepts 3 parameters
    - tag name ex: h1 // name of the tag
    - object- contains attributes to be applied on h1
    - inner content of tag or children of tag ex
    - ```
        const heading = React.createElement('h1',{id:'heading'}, 'hello from react');
        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(heading)      //anything which was under root htmlelement will be replaced by react render
      ```
- in above example render method is converting the react element to h1 tag and add it inside root element.
- Above method to create html elements in react will have very messy non-readable if we have to develop complex html strucuture.
- we can use react in very small component/section as well like here we only used inside root

***

### Webpack 
- bundler for JS application
- Power our app with different functionalities :
    - Dev build
    - Local Server
    - HMR = Hot Module Replacement // automatically updates browser window if any change is made
      - allows developers to update modules in the browser without a full reload.
      - improves the developer experience and speed during development
   as you can see your changes instantly without losing the current state of your application.
    - Faster Builds - Caching // when we build our project parcel caches the files in .parcel-cache
    - Image optimization
    - Minification
    - Bundling
    - Compress
    - Consistent hashing
    - Code splitting
    - Differential Bundling // gives support for older browser
    - Tree shaking // remove unused code
      - comes from the concept of shaking a tree to remove dead leaves, leaving only the necessary branches and leaves
      - it is a technique used in JavaScript development to remove unused code (or "dead code") from the final bundle.
      - Tree shaking is important for reducing the size of the final bundle

***

### Q: What is the dist folder?

A: 
- directory commonly used in web development projects to store the final build of the project.
- contains optimized and minified versions of the source code, ready for deployment to a production environment.

***

### Q: What is JSX

A: 
- syntax which is easier to create reactElement
- jsx is not html , not react 
- it is a HTML like syntax
- it is transpiled(converted into code that js engine understands) 
    by parcel(babel: js compiler / transpiler) before it reaches JSengine
- JSX => React.createElement => ReactElement(JS Object) => HTMLElement(render)
- babel convertes JSX to React.createElement
- to give attribute inside jsx we need to use camelCase
- JSX in multiple lines
```
const heading = (<h1 
    id="heading" 
    className="red">
        Namaste using JSX
    </h1>)
```

- JSX prevent cross site scripting ex: `{data}` where data is from attacker - jsx will sanitize it

***

### Q: React createElement vs JSX

A: 
- JSX provides more readability.
- Behind the scenes JSX is converted into react.createElement only using babel
- React.createElement
```
const element = React.createElement('div', { className: 'my-class' }, 'Hello, world!');

```

- JSX
```
const element = <div className="my-class">Hello, world!</div>;

```

***

### Q: Behind the scenes of JSX

A: JSX => React.createElement => ReactElement(JS Object) => HTMLElement(render)

***

### Q: super Power of JSX

A: 
- easy to maintain and debug code
- You can write JS in it using `{}`
```
const heading = <h1> my age is {2024-1997} </h1>
```

***

### Components

2 types:
- 1. Class Based Component //old way 
- 2. Functional Component // new way

#### Functional Components
- js function that returns JSX
- should start with capital alphabet
```
const HeadingComponent = () => {
    return <h1 id="heading" className="red">Namaste using JSX2</h1>
}
root.render(<HeadingComponent />)
```

#### Component Compositon
- composing component inside component
```
const TitleComponent = () => {
  return <h1 id="title">Namaste Title</h1>;
};

const HeadingComponent = () => (
  <div id="container">
    <TitleComponent/>
    <h1 id="heading" className="red">
      Namaste using JSX2
    </h1>
  </div>
);
```

***

### Q: {TitleComponent} vs {<TitleComponent/>} vs {<TitleComponent></TitleComponent>} in JSX.

A:
- `{TitleComponent}` with this we can embed any js variable inside our component
- js variable can contain JSX
```
const TitleEle = <h1> hi </h1>

const TryComponent = () => (
  <div id="container">
    {TitleEle}
  </div>
);
```

- `{<TitleComponent/>}` we can embed component using this inside jsx/component
```
const TitleEle = <h1> hi </h1>

const TryComponent = () => (
  <div id="container">
    {TitleEle}
  </div>
);

const anotherComponent = () => {
    <div>
        {<TitleEle/>}
    </div>
}
```

- `{<TitleComponent></TitleComponent>}`

`{<TitleComponent></TitleComponent>} = {<TitleComponent/>}`

***

### Q: is jsx mandatory for React?

A:
jsx is not mandatory - we can use React.CreateElement as well.
we use jsx because of readability and managability

***
### Q:  Is ES6 mandatory for React?

A: 
ES6 is not mandatory for React but is highly recommendable.
provides a lot of good features like - let,const,arrow functions, classes

***
### Comments in JSX
{/*  */} - for single or multiline comments
```
  {/* this is a comment */}
  {/*
         this 
        is a 
        comment
         */}
```

***

### Q: What is <React.Fragment></React.Fragment> and <></>?

A:

- <React.Fragment></React.Fragment> is a feature in React that allows you to return multiple elements
 from a React component by allowing you to group a list of children without adding extra nodes to the DOM.

- <></> is the shorthand tag for React.Fragment

- The only difference between them is that the shorthand version does not support key and props

```
// Using the empty tag shorthand
const ComponentWithEmptyTag = () => (
  <>
    <h1>Hello</h1>
    <p>World</p>
  </>
);

<React.Fragment key={fragmentKey} className="my-fragment">
  {/* Children elements */}
</React.Fragment>
```

***

### Q: Why do we need keys in React?
A:

warning: each child in the list should have unique key property
whenever you are looping over a list - always give a unique key

why ?

when there are components on same level they needs to be uniquely represented
consider a new item is added in the list - react will exactly know 
items with key that already existed, so that means only new item needs to be rendered
If we dont use key react wont know which item is added , so whole list will be rendered causing big hit on performance

```
<li key={0}>1</li>
<li key={1}>2</li>
<li key={2}>3</li>
```

***

### Q: Can we use index as keys in React?

A: 
- Yes but its a bad practice
- never use index as key - bad practice - as index might change

***

### Q: What is props in React?
A:

- props stands for properties.
- props are just like normal arguments to a function
```
function App() {
  return (
    <div className="App">
      <RestrauntCard restrauntName="donuts" /> // restrauntName is props
    </div>
  )
}
```
***
### Q: What is Conditional Rendering? explain with a code example.

A:

rendering based on a condition
```
// Using Ternary operator as a shorthand way or writing an if-else statement
{isLoggedIn ? (return <UserGreeting />) : (return <GuestGreeting />)};
```



***

### Q: What are React Hooks?

A
- React Hooks are simple JavaScript functions that let you use React features without writing a class.
- Hooks can be stateful and can manage side-effects

***
### Q: Why do we need useState Hook?

A:
- useState hook is used to maintain the state in our React application.
- Constantly watches this variable for a change via set method
- whenever a change is found react start reconcialiation algorithm

- how to import
```
import React, { useState } from "react";
```

- how to create
```
const [state, setState] = useState(initialstate);
```

***

### Q: Why do we need a useEffect Hook?

A:

- useEffect Hook is javascript function provided by react.
- It can be triggered as side effect of say fetch api
- useEffect accepts two arguments, a callback function and a dependency array.
  The second argument is optional.
```
  useEffect(() => { fetchData() }, []);
```

```
useEffect(() => {
        effect
        return () => {
            cleanup
        }
    }, [input])
```

***

### Q: How will useEffect behave in diff scenarios

A:
- if no dependency array => useEffect is called on every component render
- if the dependency array is empty = [] => useEffect is called on initial render(only called once)
- if we have something as dependency array => useEffect is called everytime dependency is changed
***

### Class components
- extends React.Component
- have a built-in state object
- ```
  class Example extends React.Component{
    constructor(props){
      super(props);
      this.state = {counter: 0}
    }

    render(){
      return <h1>hey</h1>
    }
  }
  ```

***

### Q: What is the order of life cycle method calls in Class Based Components?

A:

Following is the order of life cycle method in class bases components -
1. constructor
2. render
3. componentDidMount
4. componentDidUpdate
5. componentWillUnmount
![Screenshot 2024-03-15 at 4 05 09 PM](https://github.com/rhythm55/Namaste-react-restart/assets/36883992/29bd3481-bf11-4a9d-a104-7a5f34a6afa9)
***

### class component parent-child flow
-parent child case :
```
- parent constructor
- parent render
- child constructor
- child render
- child component did mount
- parent component didmount
```
-parent multiple child:
```
-Parent constructor
-Parent render

    - child1 constructor
    - child1 render

    - child2 constructor
    - child2 render

    <!-- DOM UPDATED IN SINGLE BATCH - react optimisation
    it is done by react as Dom manipulation/updation is expensive 
        react batches the COMMIT PHASE for children
    -->
    - child1 componentDidMount
    - child2 componentDidMount

- Parent componentDidMount
```

***

### Q: Why do we use componentDidMount?

A:
- it is a lifecycle method called once component is mounted
- allows us to execute the React code when the component is already placed in the DOM 
- Helpful when we have to call api's or need to update the state

***

### Q: Why do we use componentWillUnmount? Show with example.

A:

- `componentWillUnmount` is called before destroying the component.
- useful for the cleanup of the application

example - 
we set a timer inside componentDidMount inside about page
```
  componentDidMount() {
    // console.log("child componentDidMount called");
    this.timer = setInterval(() => {
      console.log("i was called");
    }, 1000);
  }
```
Now ,if we move to other pages like contact or home - counter will still be there
reason is because its a SPA , we are refreshing the components hence setInterval remains intact
Now to cleanup above we can use componentWillUnmount
```
  componentWillUnmount() {
    clearInterval(this.timer);
  }
```
In above as soon as we move to next component say home page - component will be destoryed
before destorying componentWillUnmount will be called and clearInterval executes

***

### Q:Why do we use super(props) in constructor?

A:

- super(props) is used to inherit the properties and access of variables 
 of the React parent class when we initialize our component.
- The main difference between super() and super(props) is the this.props
 is undefined in child's constructor in super()
 but this.props contains the passed props if super(props) is used.

***

# higher order component
- pure functions
- takes a existing component enhances it and returns the component
- used for enhacing

- Higher order component
  ```
    export const withPromoteLabel = (RestrauntCard) => {
      return (props) => {
        // returns component
        return (
          // component returns jsx
          <>
            <div className="promoted">Promoted</div>
            <RestrauntCard {...props} />
          </>
        );
      };
    };
  ```
- Higer order component invocation
  ```
   const RestrauntCardPromoted = withPromoteLabel(RestrauntCardComponent);

   return <RestrauntCardPromoted name="xyz" description="desc goes here"/>
  ```
***
### Pure Components
- Component that renders the same output for the same state and props
- skips re-renders for same props and state

- Pure function component using memo
- ### memo:
    - lets you skip re-rendering a component when its props are unchanged.
    - `memo(Component, arePropsEqual?)`
  - ```
    import React, { memo } from 'react';
  
    function Greeting({ message }) {
        return (
          <div>
            <h6>{ message }</h6>
          </div>
        )
      }
      
      // Wrap component using `React.memo()`
      export default memo(Greeting);
    ```
  - custom bailout condition
    ```
      function arePropsEqual(prevProps, nextProps) {
        return prevProps.label === nextProps.label; 
      }
      
      // Wrap component using `React.memo()` and pass `arePropsEqual`
      export default memo(PercentageStat, arePropsEqual);
    ```
  
- Pure class component
  ```
    import { PureComponent } from 'react';
  
    class Greeting extends PureComponent {
      render() {
        return <h1>Hello, {this.props.name}!</h1>;
      }
    }
  ```
***

### controlled vs uncontrolled component

- Controlled Component
    - the form data is handled by a component state.
    - Changes to the form elements are controlled by the component's state, and any changes to the state are reflected in the form elements.
    - Use controlled components when you need to perform validation, modify, or react to every change of the form data.
    - ```
        const ControlledComponent = () => {
          const [value, setValue] = useState("");
        
          const handleChange = (event) => {
            setValue(event.target.value);
          };
        
          return (
            <input
              type="text"
              value={value}
              onChange={handleChange}
            />
          );
        };
      ```
- Uncontrolled Component
    - the form data is handled by the DOM itself
    - Refs are used to access the form elements directly to retrieve their values when needed.
    - Use uncontrolled components when you want a simpler approach and don't need to manage the form data in the React state.
    - In cases where you need to optimize performance and reduce the number of re-renders, uncontrolled components can be more efficient.
    - ```
        const UncontrolledComponent = () => {
          const inputRef = useRef(null);
        
          const handleClick = () => {
            alert(inputRef.current.value);
          };
        
          return (
            <>
              <input type="text" ref={inputRef} />
              <button onClick={handleClick}>Get Value</button>
            </>
          );
        };
      ```
***

### Q: When and why do we need lazy()?

A: 
- also known as chunking/code splitting / dynamic building / lazy loading / on demand loading / dynamic code
- We want to use lazy loading when we have a large application with a big size. usually e commerece website follows it.
- example: swiggy instamart - can be loaded lazily/on demand. Only load what is required
- With help of lazy loading we are able to split our code in small chunkers which are faster to load.
- when lazy loading is implemented a seprate file in dist is created and loaded when routing hits.
- in below a seprate contact.js is made in dist. when '/contact' is triggered in routing contact.js is loaded.
```
const Contact = lazy(() => import("./components/Contact"));

{
  path: "/contact",
  element: (
    <Suspense fallback="<h1>Loding...</h1>">
      <Contact />
    </Suspense>
  ),
}
```

***

### Q: What is suspense?

A: 
- Suspense is component provided by React.
- used as wrapper of component that is to be lazily loaded
- offers a fallback option in which we can pass jsx
- React Suspense is a feature that allows components to suspend rendering
while waiting for some asynchronous operation to complete, such as fetching data.

***

### Q: When do we and why do we need suspense?

A: 
- React Suspense is used to handle asynchronous operations
- ` It allows components to suspend rendering while waiting for these operations to complete, without blocking the main UI thread. `
- Data Fetching: When fetching data asynchronously, Suspense can be used to suspend rendering until the data is available.
- Code Splitting: Suspense can then be used to suspend rendering until the required code chunks are loaded, 
- Fallback UI: Suspense allows you to define a fallback UI to display while waiting for the asynchronous operation to complete. 

***

### Q: Why we got this error: A component was suspended while responding to synchronous input. This will cause the UI to be replaced with a loading indicator. To fix this, updates that suspend should be wrapped with start transition? How does suspense fix this error?

A:
- This error occurs in React when a component suspends while responding to synchronous input.
- React Suspense is a feature that allows components to suspend rendering while waiting for some asynchronous operation to complete

***

### Q: Advantages and Disadvantages of using this code splitting pattern?

A: 
Advantages
- Improved Performance: By splitting code into smaller chunks and loading them only when needed
- Optimized Resource Usage: Code splitting allows you to load only the necessary resources for a particular view or feature, 
   reducing the overall memory and network bandwidth usage of your application.
- Better User Interaction: you can prioritize rendering critical UI elements first, providing a more responsive and interactive user experience.

Disadvantage:
- Complexity: Implementing code splitting and managing the asynchronous loading of modules can add complexity to your codebase.
- Debugging: It can be harder to trace errors that occur in dynamically loaded modules.


***

### Q: What is lifting the state up ?

A:
- In scenario where we want the state of two or more component to always change together we can use lifting the state up concept.
- In this concept we following these steps
  - remove state from both components
  - move it to their closest parent
  - pass it down to them via props
- example
```
//Parrent.js
const [showItemIndex, setShowItemIndex] = useState(0);  // moved state to closest parent

<div>
  {resInfo?.restrauntMenu?.map((menu, index) => (
      <RestaurantCategory
        key={menu.card.card.title}
        data={menu.card.card}
        showItem={showItemIndex === index}               //pass it down to them via props
        setShowItemIndex={() => setShowItemIndex(index)}   
      />
    ))}
</div>


//RestaurantCategory.js
const RestaurantCategory = ({ data, showItem, setShowItemIndex }) => {
  const handleClick = () => {
    setShowItemIndex();  
  };
<div className="accordion" onClick={() => handleClick()}>
    <div className="accordion-body">
      {data.itemCards.map(
        (item) =>
          showItem && (
            <ItemList key={item.card.info.id} item={item.card.info} />
          )
      )}
    </div>
 </div>
```

***

### Prop drilling
- When we pass props from parent to child and so on in the hierarchy say 20 level down 
- prop drilling with lots of level is not a good practice - what if prop value gets changed in between
- problem if a lot of heirarchy - we can use useContex

***

### Q: What is context provider and context consumer.

A:
-`context provider`
- If we want to change the value of useContext we can use `context provider`
- the elements which are wrapped inside context.provider will get the updated value defined
- we can also pass setState method as value so that component can also be able to change the value
- example 
```
  const [userName, setUserName] = useState("Any");

   <UserContext.Provider value={{ loggedInUserName: userName, setUserName }}>
        <HeaderComponent />
        <Outlet />
   </UserContext.Provider>
```


- `context consumer`
- mainly used if we want to use useContext inside class components as they dont have hooks
- provides a callback method which returns the required context value
- example
```
 <UserContext.Consumer>
    {(data) => <h3>logged in user : {data.loggedInUserName}</h3>}
  </UserContext.Consumer>
```

***

### useContext
- React Hook that lets you read and subscribe to context from your component
- ```
    //App.js
      export const ProductContext = createContext([]);
      
      export default function App() {
        const [productList, setProductList] = useState([]);
        return (
          <>
            <ProductContext.Provider value={{ productList, setProductList }}>
              <AddComponent />
            </ProductContext.Provider>
          </>
        );
      }

    //Product.js
    const ProductComponent = () => {
      const { productList, setProductList } = useContext(ProductContext);
    }
  ```

***

### forwardRef and useImperativeHandle

- forwardRef
    - lets your component expose a DOM node to parent component with a ref.
- useImperativeHandle
  - React Hook that lets you customize the handle exposed as a ref.
  - ex: suppose you don’t want to expose the entire <input> DOM node, but you want to expose focus

```
// App.js
export default function App() {
  const nameRef = useRef(null);
  const handleFocus = () => {
    nameRef.current.focus();
  };

  return (
    <>
      <FormInput placeholder="enter your name" ref={nameRef} />
      <button onClick={() => handleFocus()}>focus</button>
  );
}


//FormInput.js
const FormInput = forwardRef(function FormInput(props, ref) {
  const inpRef = useRef(null);

  useImperativeHandle(ref, () => {
    return {
      focus() {
        return inpRef.current.focus();
      },
    };
  });

  return <input ref={inpRef} placeholder={props.placeholder} />;
});
```
***

### useMemo
- React Hook that lets you cache the result of a calculation between re-renders.
- `useMemo(calculateValue, dependencies) `
- ```
      const visibleTodos = useMemo(
          () => filterTodos(todos, tab),
          [todos, tab]
        );
  ```
***

### useCallback
-  React Hook that lets you cache a function definition between re-renders.
-   `const cachedFn = useCallback(fn, dependencies)`
    
- ```
    export default function ProductPage({ productId, referrer, theme }) {
        const handleSubmit = useCallback((orderDetails) => {
          post('/product/' + productId + '/buy', {
            referrer,
            orderDetails,
          });
        }, [productId, referrer]);
  ```    
***

### Profiler component
- lets you measure rendering performance of a React tree programmatically.
```
const Shopping = () => {
 const onRender = (
    id,
    phase,
    actualDuration,
    baseDuration,
    startTime,
    commitTime
  ) => {
    console.log("id ", id);
    console.log("phase ", phase); //"mount", "update" or "nested-update"
    console.log("actualDuration ", actualDuration); // milliseconds spent rendering the <Profiler> and its descendants
    console.log("baseDuration ", baseDuration); // milliseconds estimating how much time it would take to re-render
    console.log("startTime ", startTime);   // timestamp for when React began rendering the current update
    console.log("commitTime ", commitTime); //timestamp for when React committed the current update
  };
  return (
    <div className="shopping-container">
      <Profiler id="shopping" onRender={onRender}>
          <ItemList />
      </Profiler>
    </div>
  );
};
```

***

## React router
- we use library `react-router-dom`
- `BrowserRouter` is a router implementation that uses the HTML5 history API (pushstate, replacestate, and popstate events) to keep your UI in sync with the URL
- ```
    const appRoutes = createBrowserRouter([
      {
        path: '/',
        element: <App/>,
        children: [
          {
            path: '/contact',
            element: <Contact/>,
            errorElement: <Error/>
          }
        ]
      }
    ])
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<RouterProvider  router={appRoutes}/>)

  // anywhere in application
   <Link to="/contact">Contact us</Link>
  ```
- another way
  ```
    //index.js
      <BrowserRouter>
        <App />
      </BrowserRouter>

    //app.js
    function App() {
        return (
          <div className="container">
            <nav>
              <ul>
                <Link to="/" class="list">
                  Home
                </Link>
              </ul>
            </nav>
      
            <Routes>
              <Route path="/" element={<Home />} />
            </Routes>
          </div>
        );
      }
  ```
***

### React testing 

***
