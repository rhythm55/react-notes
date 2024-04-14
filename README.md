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
