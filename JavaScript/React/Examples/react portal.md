## React Portal Example Script
```js
// App.js
import React from 'react';
import WindowPortalOne from './WindowPortalOne';
import WindowPortalTwo from './WindowPortalTwo';

class App extends React.PureComponent {
  constructor(props) {
    super(props);
    
    this.state = {
      counter: 0,
      showWindowPortalOne: false,
      showWindowPortalTwo: false,
      windowWidth: 600,
      windowHeight: 400,
    };
  }

  componentDidMount() {
    window.addEventListener('beforeunload', () => {
      this.closeWindowPortal();
    });
    
    window.setInterval(() => {
      this.setState(state => ({
        counter: state.counter + 1,
      }));
    }, 1000);
  }
  
  toggleWindowPortalOne = () => {
    this.setState(state => ({
      ...state,
      showWindowPortalOne: !state.showWindowPortalOne,
    }));
  }

  toggleWindowPortalTwo = () => {
    this.setState(state => ({
      ...state,
      showWindowPortalTwo: !state.showWindowPortalTwo,
    }));
  }
  
  closeWindowPortalOne = () => {
    this.setState({ showWindowPortalOne: false })
  }

  closeWindowPortalTwo = () => {
    this.setState({ showWindowPortalTwo: false })
  }
  
  render() {
    return (
      <div>
        <h1>Counter: {this.state.counter}</h1>
        
        <button onClick={this.toggleWindowPortalOne}>
          {this.state.showWindowPortalOne ? 'Close the' : 'Open a'} Portal One
        </button>

        <button onClick={this.toggleWindowPortalTwo}>
          {this.state.showWindowPortalTwo ? 'Close the' : 'Open a'} Portal Two
        </button>
        
        {this.state.showWindowPortalOne && (
          <WindowPortalOne 
            closeWindowPortalOne={this.closeWindowPortalOne} 
            counter={this.state.counter} 
            windowWidth={this.state.windowWidth}
            windowHeight={this.state.windowHeight}
          />
        )}

        {this.state.showWindowPortalTwo && (
          <WindowPortalTwo
            closeWindowPortalTwo={this.closeWindowPortalTwo} 
            counter={this.state.counter} 
            windowWidth={this.state.windowWidth}
            windowHeight={this.state.windowHeight}
          />
        )}
      </div>
    );
  }
}

export default App;
```
```css
// index.css
body {
  font-family: -apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",sans-serif;
  font-size: 20px;
  background: #1e1f20;
  color: #eee;
}

h1 {
  font-weight: 400;
}

button {
  padding: 8px 16px;
  background: crimson;
  color: white;
  border: none;
  font-size: inherit;
  margin-right: 10px;
}
```
```js
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App/>, document.getElementById('root'));
serviceWorker.unregister();
```
```js
// WindowPortalOne.js
import React from 'react';
import ReactDOM from 'react-dom';

function copyStyles(sourceDoc, targetDoc) {
  Array.from(sourceDoc.styleSheets).forEach(styleSheet => {
    if (styleSheet.cssRules) { // true for inline styles
      const newStyleEl = sourceDoc.createElement('style');

      Array.from(styleSheet.cssRules).forEach(cssRule => {
        newStyleEl.appendChild(sourceDoc.createTextNode(cssRule.cssText));
      });

      targetDoc.head.appendChild(newStyleEl);
    } else if (styleSheet.href) { // true for stylesheets loaded from a URL
      const newLinkEl = sourceDoc.createElement('link');

      newLinkEl.rel = 'stylesheet';
      newLinkEl.href = styleSheet.href;
      targetDoc.head.appendChild(newLinkEl);
    }
  });
}


class WindowPortalOne extends React.PureComponent {
  constructor(props) {
    super(props);
    this.props = props;
    this.containerEl = document.createElement('section');
    this.externalWindow = null;
  }

  componentDidMount() {
    this.externalWindow = window.open('', '',
     `width=${this.props.windowWidth},
      height=${this.props.windowHeight},
      left=${(window.screen.width) ? (window.screen.width - this.props.windowWidth)/2 : 0},
      top=${(window.screen.height) ? (window.screen.height - this.props.windowHeight)/2 : 0}`);
    this.externalWindow.document.body.appendChild(this.containerEl);
    this.externalWindow.document.title = 'Portal Window One';
    copyStyles(document, this.externalWindow.document);

    this.externalWindow.addEventListener('beforeunload', () => {
      this.props.closeWindowPortalOne();
    });
  }

  componentWillUnmount() {
    this.externalWindow.close();
  }
  
  render() {
    return ReactDOM.createPortal(
      <article>
        <h1>Counter in the portal One: {this.props.counter}</h1> 
        <button onClick={() => this.props.closeWindowPortalOne()} >Close me!</button>
      </article>, this.containerEl);
  }
}

export default WindowPortalOne;
```
```js
// WindowPortalTwo.js
import React from 'react';
import ReactDOM from 'react-dom';

function copyStyles(sourceDoc, targetDoc) {
  Array.from(sourceDoc.styleSheets).forEach(styleSheet => {
    if (styleSheet.cssRules) { // true for inline styles
      const newStyleEl = sourceDoc.createElement('style');

      Array.from(styleSheet.cssRules).forEach(cssRule => {
        newStyleEl.appendChild(sourceDoc.createTextNode(cssRule.cssText));
      });

      targetDoc.head.appendChild(newStyleEl);
    } else if (styleSheet.href) { // true for stylesheets loaded from a URL
      const newLinkEl = sourceDoc.createElement('link');

      newLinkEl.rel = 'stylesheet';
      newLinkEl.href = styleSheet.href;
      targetDoc.head.appendChild(newLinkEl);
    }
  });
}


class WindowPortalTwo extends React.PureComponent {
  constructor(props) {
    super(props);
    this.props = props;
    this.containerEl = document.createElement('section');
    this.externalWindow = null;
  }

  componentDidMount() {
    this.externalWindow = window.open('', '',
     `width=${this.props.windowWidth},
      height=${this.props.windowHeight},
      left=${(window.screen.width) ? (window.screen.width - this.props.windowWidth)/2 : 0},
      top=${(window.screen.height) ? (window.screen.height - this.props.windowHeight)/2 : 0}`);
    this.externalWindow.document.body.appendChild(this.containerEl);
    this.externalWindow.document.title = 'Portal Window Two';
    copyStyles(document, this.externalWindow.document);

    this.externalWindow.addEventListener('beforeunload', () => {
      this.props.closeWindowPortalTwo();
    });
  }

  componentWillUnmount() {
    this.externalWindow.close();
  }
  
  render() {
    return ReactDOM.createPortal(
      <article>
        <h1>Counter in the portal One: {this.props.counter}</h1> 
        <button onClick={() => this.props.closeWindowPortalTwo()} >Close me!</button>
      </article>, this.containerEl);
  }
}

export default WindowPortalTwo;
```
Inspired By [David Gilbertson](https://medium.com/hackernoon/using-a-react-16-portal-to-do-something-cool-2a2d627b0202)
