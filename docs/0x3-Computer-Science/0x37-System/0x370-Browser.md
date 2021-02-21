# 0x371 Browser

- [1. Web API](#1-web-api)
    - [1.1. DOM](#11-dom)
        - [1.1.1. Types](#111-types)
    - [1.2. Window](#12-window)
        - [1.2.1. Storage](#121-storage)
        - [1.2.2. Timer](#122-timer)
    - [1.3. Communication API](#13-communication-api)
        - [1.3.1. XMLHttpRequest](#131-xmlhttprequest)
        - [1.3.2. Fetch API](#132-fetch-api)
        - [1.3.3. WebSocket](#133-websocket)
    - [1.4. Worker API](#14-worker-api)
- [2. Framework](#2-framework)
    - [2.1. React](#21-react)
        - [2.1.1. Element](#211-element)
        - [2.1.2. JSX](#212-jsx)
        - [2.1.3. Component](#213-component)
    - [2.2. Vue](#22-vue)
    - [2.3. Angular](#23-angular)
- [3. Implementation](#3-implementation)
        - [3.0.1. Multiprocess Architecture](#301-multiprocess-architecture)
        - [3.0.2. Memory Management](#302-memory-management)
        - [3.0.3. Renderer Model](#303-renderer-model)
        - [3.0.4. Others](#304-others)
- [4. Reference](#4-reference)

## 1. Web API
### 1.1. DOM
DOM (Document Object Model) is a cross-language programming interface for accessing and modifying HTML and XML. DOM represents the documents as nodes and objects, so that programming language can connect to the page.

#### 1.1.1. Types
**Type (Document)** the root node

$$EventTarget <- Node <- Element <- HTMLElement$$

**Type (Node)** It is an abstract base class, every object within the document is a kind of Node.

**Type (Element)** Element is based on Node, it is the most general base calss from which all element objects in a Document inherits

**Type (NodeList)** A collection of nodes

### 1.2. Window
All global objects, functions, variables is the member of Window (even document)

#### 1.2.1. Storage
Browser can store key/value pairs for each origin, (other way is to store in cookie)

- SessionStorage: available during the page sesssion (as long as browser is open)
- LocalStorage: persists even browser is closed

#### 1.2.2. Timer
Window (or other scopes) can have timer
- setTimeout: set timer
- clearTimeout: clear timer


### 1.3. Communication API

#### 1.3.1. XMLHttpRequest
Objects used to interact with servers, used heavily in AJAX.

#### 1.3.2. Fetch API
Promised based API

#### 1.3.3. WebSocket
API which enables two-way interactive communication


### 1.4. Worker API
Parallelism within JavaScript!!!

Supported from HTML5, each worker is running in a different Thread.

## 2. Framework
### 2.1. React
minimalist framework.


#### 2.1.1. Element
**Type (React element)** A react element is a JavaScript object referring to a piece of the User Interface, it is passed to other libraries (e.g: React DOM)to be converted into native elements (e.g. DOM)

```javascript
React.createElement(
    'type',
    { properties },
    [children ... ]
)
```

#### 2.1.2. JSX
**JSX** stands for JavaScript XML. It is an extension for JavaScript that serves as a shortcut for calling `React.createElement` to create element and components.


According to the official page, JSX is an XML-like syntax extension to ECMAScript without any defined semantics. It's NOT intended to be implemented by engines or browsers. It's NOT a proposal to incorporate JSX into the ECMAScript spec itself.

```javascript
// equivalent statements
const element = <h1>Hello, world</h1>;
const element = React.createElement('h1', null, 'Hello World');
```


#### 2.1.3. Component
**React Component** A React component is a function or class that returns a valid React element.

state: maintain the observable data, when updated, the associated items will be rendered again. This should be treated as immutable. Use setState to update state

### 2.2. Vue
between angular & react

### 2.3. Angular
everything built-in

## 3. Implementation
Summary of implementations and architecture related to browsers engines, in particular, blink (chromium's engine)

#### 3.0.1. Multiprocess Architecture

- browser process: the main process which hosts UI and manages tab, plugin processes
- renderer process: tab-specific process, can IPC with browser process, contained in sandbox (for security). Each iframe is separated into one process (site-isolation)

#### 3.0.2. Memory Management

- GC: oilpan
  
#### 3.0.3. Renderer Model

Blink's renderer is a stage-based engine, easy to implement partial invalidation

- Stage 1: parse HTML into DOM tree
- Stage 2: apply CSS style to DOM
- Stage 3: compute layout (x, y coordinate) for each element, building layout tree
- Stage 4: partition regions into independent layers
- Stage 5: raster

#### 3.0.4. Others
- Chrome source code is around 25m lines (Linux kernel has 28m)

## 4. Reference

[1] [Mozilla MDN Documentations](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)