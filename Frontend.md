# Dependencies and Comparison

## Requirements:
* XSS and CSRF protection
* OSS friendly: i.e. allows public code, public work items, public build logs, - all the information can be accessed anonymously
* Easy to setup and easy to develop. Lot of documentation and examples
* Provide fast initial rendering and delta updates of DOM elements
* Integration with GitHub, e.g. code is hosted in GitHub, and every Pull Request and every Branch are built automatically (e.g. using webhooks).
* The development setup is not couple to Windows, a developer can work on Windows, MacOS and Linux

### Webframework

|                | SEC | KISS | REQ | MAT | REL | PERF | COST |
|----------------|-----|------|-----|-----|-----|------|------|
| ~~Angular~~    |  Y  |   N  |  N  |  2  |  2  |  2   |      |
| ~~Knockout~~   |  Y  |   Y  |  N  |  1  |  2  |  1   |      |
| React          |  Y  |   Y  |  Y  |  3  |  3  |  3   |      |

* Based on above criteria React definitely comes out as a winner. 
* The framework provides view and is flexible to work with other frameworks when comes to services, DI, routing, state management, test etc.
* We can start small and add additional complexity to the framework the business decisions or requirements change.

### Layout Management
|                            | SEC | KISS | REQ | MAT | REL | PERF | COST |
|----------------------------|-----|------|-----|-----|-----|------|------|
| ~~Goldenlayout~~           |     |  Y   |  N  |  1  |  1  |  3   |  3   |
| ~~Isotope~~                |     |  Y   |  N  |  3  |  2  |  3   |  3   |
| ~~json layout(internal)~~  |     |  Y   |  N  |  1  |  1  |  2   |  3   |
| ~~Masonry~~                |     |  Y   |  N  |  3  |  2  |  3   |  3   |
| ~~phosphorjs~~             |     |  N   |  N  |  1  |  1  |  3   |  3   |
| react-bootstrap(bootstrap) |     |  Y   |  Y  |  3  |  3  |  3   |  3   |

* Based on what are current requirements are bootstrap gives a lot more and is the de facto standard when comes to 
web development
* What makes it even more attractive is the react-bootstrap that seamlessly merges in with our react framework
* Both have extensive documentation [react-bootstrap](https://react-bootstrap.github.io/components.html) and [bootstrap](http://getbootstrap.com/components/)

### Routing

* react-router is definitely the best option we have that works very well w/o any real setup with the react framework
* For routing requirements there are certain stand-alone routers that work with any frameworks like crossroads and navigo. But none of them have any compelling reason to be even considered.

### State management

|                 | SEC | KISS | REQ | MAT | REL | PERF | COST |
|-----------------|-----|------|-----|-----|-----|------|------|
| PubSubJs        |     |  Y   |  Y  |  2  |  2  |  2   |  3   |
| react-flux      |     |  Y   |  Y  |  3  |  2  |  2   |  3   |
| react-redux     |     |  Y   |  Y  |  3  |  3  |  3   |  3   |
