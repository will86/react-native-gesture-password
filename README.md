# react-native-gesture-password

A gesture password component for React Native. It supports both iOS and Android since it's' written in pure JavaScript.

一个React Native的手势密码组件，纯JavaScript实现，因此同时支持iOS和安卓平台。

![image](https://github.com/Spikef/react-native-gesture-password/raw/master/screenshot.gif)

## Install

```javascript
npm install react-native-gesture-password --save
```

## Properties

All properties bellow are optional.

### message (string)

The message text you want to show.

### status (string)

Can be 'normal', 'right' or 'wrong'.

The gesture password don't validate your password. You should do that yourself, and tell the result by status.

### style (string)
Styles for the gesture password view.

### rightColor (string)

Use this color to render when status !== 'wrong'.

### wrongColor (string)

Use this color to render when status === 'wrong'.

### interval (number)

The active circles will be reset automatically after you give an interval.

### onStart (function)

Event raised when user touch a number circle.

### onEnd (function)

Event raised when user finish input a password.

### children

Other components that you want to display.

## Examples

```javascript

var React = require('react-native');
var {
    AppRegistry,
    } = React;

var PasswordGesture = require('react-native-gesture-password');

var Password1 = '';
var AppDemo = React.createClass({
    // Example for check password
    onEnd: function(password) {
        if (password == '123') {
            this.setState({
                status: 'right',
                message: 'Password is right, success.'
            });

            // your codes to close this view
        } else {
            this.setState({
                status: 'wrong',
                message: 'Password is wrong, try again.'
            });
        }
    },
    onStart: function() {
        this.setState({
            status: 'normal',
            message: 'Please input your password.'
        });
    },

    // Example for set password
    /*
    onEnd: function(password) {
        if ( Password1 === '' ) {
            // The first password
            Password1 = password;
            this.setState({
                status: 'normal',
                message: 'Please input your password secondly.'
            });
        } else {
            // The second password
            if ( password === Password1 ) {
                this.setState({
                    status: 'right',
                    message: 'Your password is set to ' + password
                });

                Password1 = '';
                // your codes to close this view
            } else {
                this.setState({
                    status: 'wrong',
                    message:  'Not the same, try again.'
                });
            }
        }
    },
    onStart: function() {
        if ( Password1 === '') {
            this.setState({
                message: 'Please input your password.'
            });
        } else {
            this.setState({
                message: 'Please input your password secondly.'
            });
        }
    },
    */

    getInitialState: function() {
        return {
            message: 'Please input your password.',
            status: 'normal'
        }
    },
    render: function() {
        return (
            <PasswordGesture
                ref='pg'
                status={this.state.status}
                message={this.state.message}
                onStart={() => this.onStart()}
                onEnd={(password) => this.onEnd(password)}
                />
        );
    }
});

AppRegistry.registerComponent('AppDemo', () => AppDemo);

```
## Change Logs

v1.0.2 Improve the performance for real device.

v1.0.0 Rewrite in pure javascript, for Android support.

## Notes

This old version(<0.1.0) is at the branch native. I won't update that unless fix bugs.

If you have suggestions or bug reports, feel free to send pull request or [create new issue](https://github.com/spikef/react-native-gesture-password/issues/new).
