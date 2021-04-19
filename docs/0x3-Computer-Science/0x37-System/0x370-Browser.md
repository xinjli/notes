# 0x370 Browser

- [1. History](#1-history)
- [2. Web API](#2-web-api)
    - [2.1. DOM](#21-dom)
        - [2.1.1. Types](#211-types)
    - [2.2. Window](#22-window)
        - [2.2.1. Storage](#221-storage)
        - [2.2.2. Timer](#222-timer)
    - [2.3. Communication API](#23-communication-api)
        - [2.3.1. XMLHttpRequest](#231-xmlhttprequest)
        - [2.3.2. Fetch API](#232-fetch-api)
        - [2.3.3. WebSocket](#233-websocket)
    - [2.4. Worker API](#24-worker-api)
- [3. Framework](#3-framework)
    - [3.1. React](#31-react)
        - [3.1.1. Element](#311-element)
        - [3.1.2. JSX](#312-jsx)
        - [3.1.3. Component](#313-component)
    - [3.2. Vue](#32-vue)
    - [3.3. Angular](#33-angular)
- [4. Implementation](#4-implementation)
        - [4.0.1. Multiprocess Architecture](#401-multiprocess-architecture)
        - [4.0.2. Memory Management](#402-memory-management)
        - [4.0.3. Renderer Model](#403-renderer-model)
        - [4.0.4. Others](#404-others)
- [5. Reference](#5-reference)


## 1. History

A short timeline of major browsers

- 1993: Mosaic (by Marc Andreessen and Eric Bina) 
- 1994: Netscape Navigator (same developers as Mosaic, introducing JavaScript)
- 1995: IE (from Windows 95)
- 1995: Opera
- 1998: KHTML (browser engine developed by the KDE project)
- 2002: Firefox (spiritual successor of Netscape Navigator)
- 2003: Safari (engine is WebKit, fork of KHTML)
- 2008: Chrome (engine is Blink, fork of WebKit)
- 2015: Edge (from Windows 10, chromium based now)
- 

## 2. Web API
### 2.1. DOM
DOM (Document Object Model) is a cross-language programming interface for accessing and modifying HTML and XML. DOM represents the documents as nodes and objects, so that programming language can connect to the page.

#### 2.1.1. Types
**Type (Document)** the root node

$$\text{EventTarget} \to \text{Node} \to \text{Element} \to \text{HTMLElement}$$

**Type (Node)** It is an abstract base class, every object within the document is a kind of Node.

**Type (Element)** Element is based on Node, it is the most general base calss from which all element objects in a Document inherits

**Type (NodeList)** A collection of nodes

### 2.2. Window
All global objects, functions, variables is the member of Window (even document)

#### 2.2.1. Storage
Browser can store key/value pairs for each origin, (other way is to store in cookie)

- SessionStorage: available during the page sesssion (as long as browser is open)
- LocalStorage: persists even browser is closed

#### 2.2.2. Timer
Window (or other scopes) can have timer
- setTimeout: set timer
- clearTimeout: clear timer


### 2.3. Communication API

#### 2.3.1. XMLHttpRequest
Objects used to interact with servers, used heavily in AJAX.

#### 2.3.2. Fetch API
Promised based API

#### 2.3.3. WebSocket
API which enables two-way interactive communication


### 2.4. Worker API
Parallelism within JavaScript!!!

Supported from HTML5, each worker is running in a different Thread.

## 3. Framework
### 3.1. React
minimalist framework.


#### 3.1.1. Element
**Type (React element)** A react element is a JavaScript object referring to a piece of the User Interface, it is passed to other libraries (e.g: React DOM)to be converted into native elements (e.g. DOM)

```javascript
React.createElement(
    'type',
    { properties },
    [children ... ]
)
```

#### 3.1.2. JSX
**JSX** stands for JavaScript XML. It is an extension for JavaScript that serves as a shortcut for calling `React.createElement` to create element and components (It is transpiled to createElement)


According to the official page, JSX is an XML-like syntax extension to ECMAScript without any defined semantics. It's NOT intended to be implemented by engines or browsers. It's NOT a proposal to incorporate JSX into the ECMAScript spec itself.

```javascript
// equivalent statements
const element = <h1>Hello, world</h1>;
const element = React.createElement('h1', null, 'Hello World');
```

Within JSX tags, we can only write JSX tags, not normal JavaScript. In order to write JavaScript, we use curly braces to tell the transpiler to process what is between the curly braces as normal JavaScript

```javascript
const Welcome = () => {
    const name = 'JavaScript';
    return <p>Welcome {name}!</p>
}
```


#### 3.1.3. Component
**React Component** A React component is a function or class that returns a valid React element.

state: maintain the observable data, when updated, the associated items will be rendered again. This should be treated as immutable. Use setState to update state

### 3.2. Vue
between angular & react

### 3.3. Angular
everything built-in

## 4. Implementation
Summary of implementations and architecture related to browsers engines, in particular, blink (chromium's engine)

#### 4.0.1. Multiprocess Architecture

- browser process: the main process which hosts UI and manages tab, plugin processes
- renderer process: tab-specific process, can IPC with browser process, contained in sandbox (for security). Each iframe is separated into one process (site-isolation)

#### 4.0.2. Memory Management

- GC: oilpan
  
#### 4.0.3. Renderer Model

Blink's renderer is a stage-based engine, easy to implement partial invalidation

- Stage 1: parse HTML into DOM tree
- Stage 2: apply CSS style to DOM
- Stage 3: compute layout (x, y coordinate) for each element, building layout tree
- Stage 4: partition regions into independent layers
- Stage 5: raster

#### 4.0.4. Others
- Chrome source code is around 25m lines (Linux kernel has 28m)

## 5. Reference

[1] [Mozilla MDN Documentations](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)