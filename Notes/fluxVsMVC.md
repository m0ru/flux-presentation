# Flux Implementations

some mix flux-architecture with efficient rendering (e.g. jFlux), reducing modularity

all offer control over the circular data-flow

![flux diagram](http://facebook.github.io/react/img/blog/flux-diagram.png)

{<deloreanjs.com> has a good, simple example suited for demo-ing}

* [jFlux-slides @ mvc](http://slides.com/christianalfoni/deck--3/#/14)
* [jFlux-slides @ backbone architecture](http://slides.com/christianalfoni/deck--3/#/16)
* [jFlux-slides @ angular p18ff](http://slides.com/christianalfoni/deck--3/#/18)
* [jFlux-slides @ facebook flux architecture](http://slides.com/christianalfoni/deck--3/#/27)
* fazit: mvc good for small apps, bad if there's a lot of app state / it doesn't scale well

* Facebook Flux
* [jFlux](https://www.youtube.com/watch?v=plUN2L4Ak14)
    * 34kB min'd, 12kB gzip'd, 
    * to be used with jQuery
    * virtual dom
    * components
    * routing
* [Delorean.js](http://deloreanjs.com/) 
    * 18kB min'd, 7kB gzip'd
    * view-agnostic
    * plugins to ease connecting with React, Flight and Ractive
    * UI-data "rollbacks" (?) (~transactions?)
* flux-action
* compose-flux-dispatcher
* react-flux
* fluxxor
* reflux
* dispatchr

# View Libraries

These are agnostic to how routing or (server-/side)-templating is handled. In some cases they come with implementations that can be defaulted to but aren't mandatory.

They tend to keep all parts of the component in a single file (at least flux/riot)

* React 
    * by FB 
    * jsx templating (= js + inline html)
    * server-side rendering
    * virtual dom
    * doesn't do:
        * An event system (other than vanilla DOM events)
        * Any AJAX capabilities whatsoever
        * Any form of a data layer
        * Promises
        * Any application framework at all
        * Any idea how implement the above
* Riot
    * 8.8kB min'd, 4.3kB gzip'd
    * aims to replace React
    * virtual dom
* [Ractive.js](http://www.ractivejs.org/) 
    * by The Guardian
    * 162kB min'd, 60.8kB gzip'd
* [Flight.js](http://flightjs.github.io/) 
    * by Twitter
    * 14kB min'd, 5.5kB gzip'd
    * components
    * events (uses dom event bubbling)
    * depends on jQuery(82kB) and webpack/requirejs
    * stays close to regular dom

most of the above will require ES5 shim - a polyfill to support IE8

# Blogs/Quotes:

## Reactjs for Stupid People

<http://blog.andrewray.me/reactjs-for-stupid-people/>

**@ jsx:** You can always tell how your component will render by looking at one source file. 

""" html
<header>  
   <div class="name"></div>
</header>  
""" 

""" javascript
$.post('/login', credentials, function( user ) {
    // Modify the DOM here
    $('header .name').show().text( user.name );
});
"""

versus

""" jsx
render: function() {  
    return <header>
        { this.state.name ? <div>this.state.name</div> : null }
    </header>;
}
"""
    
    
**@ jsx:** Traditionally you separate views (HTML) from functionality (Javascript). This leads to monolithic Javascript files containing all functionality for one "page", and you have to trace complex flow from JS > HTML > JS > bad-news-sad-time.

**@ flux:** The concept "Flux" is simply that your view triggers an event (say, after user types a name in a text field), that event updates a model, then the model triggers an event, and the view responds to that model's event by re-rendering with the latest data. That's it. 

**@ flux:** This one way data flow / decoupled observer pattern is designed to guarantee that your source of truth always stays in your stores / models.

**@ pros & cons of react:**

Here's why you should use React:

    * Works great for teams, strongly enforcing UI and workflow patterns
    * UI code is readable and maintainable
    * Componentized UI is the future of web development, and you need to start doing it now.

Here's why you should think twice before you switch:

    * React will **slow you down tremendously** at the start. Understanding how props, state, and component communication works is not straightforward, and the docs are a maze of information. This will be countered, in theory, by a grand speed up when your whole team is on board.
    * React does not support any browser below IE8, and never will
    * If your application / website doesn't have very much dynamic page updating, you will be implementing a lot of code for a very small benefit.
    * You will reinvent a lot of wheels. React is young, and because there's no canonical way to do events / component communication, you'll have to build large component libraries from scratch. Does your application have dropdowns, resizable windows, or lightboxes? You'll probably have to write those all from scratch.
        * {note: there's wrappers/components for most things already, e.g. jquery, bootstrap,...}



