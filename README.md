# react-router-bootstrap

Intregation between [react-router](https://github.com/rackt/react-router) and [react-bootstrap](https://github.com/react-bootstrap/react-bootstrap)

This package gives you a `NavItemLink` and `ButtonLink` which are substitutes for react-router's `NavItem` and `Button`

Turning this:

```jsx
React.createClass({
  mixins: [State, Navigation],

  render: function() {
    var href = this.makeHref('destination', {some: 'params'}, {some: 'query param'});
    var isActive = this.isActive('destination', {some: 'params'}, {some: 'query param'});
    return <Button href={href} active={isActive}>;
  }
});
```

Into this

```jsx
React.createClass({
  render: function() {
    return <ButtonLink to="destination" some="params" query={{some: 'query param'}}>;
  }
});
```

## Installation

<table>
  <tr>
    <th>react 0.11.x</th>
    <td>`npm install --save react-router-bootstrap@~0.6`</td>
  </tr>
  <tr>
    <th>react 0.12.x</th>
    <td>`npm install --save react-router-bootstrap@~0.7`</td>
  </tr>
</table>

You will also (if you haven't already) want to install `react-router` and `react-bootstrap`

```
npm install --save react-router react-bootstrap
```


## Usage

A simple example for **react 0.12.x**

```jsx
var Router = require('react-router')
  , RouteHandler = Router.RouteHandler
  , Route = Router.Route;

var ReactBootstrap = require('react-bootstrap')
  , Nav = ReactBootstrap.Nav;

var ReactRouterBootstrap = require('react-router-bootstrap')
  , NavItemLink = ReactRouterBootstrap.NavItemLink
  , ButtonLink = ReactRouterBootstrap.ButtonLink;

var App = React.createClass({
  render: function() {
    return (
      <div>
        NavItemLink<br />
        <Nav>
          <NavItemLink
            to="destination"
            someparam="hello">
            Linky!
          </NavItemLink>
        </Nav>
        <br />
        ButtonLink<br />
        <ButtonLink
          to="destination"
          someparam="hello">
          Linky!
        </ButtonLink>
        <RouteHandler />
      </div>
    );
  }
});

var Destination = React.createClass({
  render: function() {
    return <div>You made it!</div>;
  }
});

var routes = (
  <Route handler={App} path="/">
    <Route name="destination" path="destination/:someparam" handler={Destination} />
  </Route>
);

Router.run(routes, function (Handler) {
  React.render(<Handler/>, document.body);
});

```

A simple example for **react 0.11.x** (make sure to give the file a .jsx extension!)

```jsx
var Router = require('react-router')
  , Routes = Router.Routes
  , Route = Router.Route;

var ReactBootstrap = require('react-bootstrap')
  , Nav = ReactBootstrap.Nav;

var ReactRouterBootstrap = require('react-router-bootstrap')
  , NavItemLink = ReactRouterBootstrap.NavItemLink
  , ButtonLink = ReactRouterBootstrap.ButtonLink;

var App = React.createClass({
  render: function() {
    var ActiveRouteHandler = this.props.activeRouteHandler;

    return (
      <div>
        NavItemLink<br />
        <Nav>
          <NavItemLink
            to="destination"
            someparam="hello">
            Linky!
          </NavItemLink>
        </Nav>
        <br />
        ButtonLink<br />
        <ButtonLink
          to="destination"
          someparam="hello">
          Linky!
        </ButtonLink>
        <ActiveRouteHandler />
      </div>
    );
  }
});

var Destination = React.createClass({
  render: function() {
    return <div>You made it!</div>;
  }
});

var routes = (
  <Routes>
    <Route handler={App} path="/">
      <Route name="destination" path="destination/:someparam" handler={Destination} />
    </Route>
  </Routes>
);

React.renderComponent(routes, document.body);
```
