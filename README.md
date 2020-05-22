# Expo Amplify broken using latest react-native-web

**Filed 2 bugs:**

<https://github.com/aws-amplify/amplify-js/issues/5865>
<https://github.com/react-native-elements/react-native-elements/issues/2368>

## Broken using "react-native-web": "~0.12.2"

`Failed to compile
D:/dev0/amplify-experiment/expo-amplify/node_modules/react-native-elements/src/config/ViewPropTypes.js
Module not found: Can't resolve 'react-native-web/dist/exports/ViewPropTypes' in 'D:\dev0\amplify-experiment\expo-amplify\node_modules\react-native-elements\src\config'`

## Works using "react-native-web": "~0.11.7"

See reason: <https://github.com/necolas/react-native-web/releases/tag/0.12.0>

Short answer: 0.12.x removed use of the prop types exports which have been deprecated in React Native.

## Installation

```
npm i -g @aws-amplify/cli
amplify configure

npm install expo-cli --global

```

### Clone/download this project, configure

```
cd expo-amplify

npm install

```

### To reproduce the error

Only aws-exports.js (included) is needed to reproduce the error

```
expo start -w

```

### To get aws auth working (not needed to reproduce error)

```
amplify init
amplify add auth
amplify push
```
