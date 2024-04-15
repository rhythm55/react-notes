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
