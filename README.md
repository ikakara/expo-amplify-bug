# Expo Amplify broken using latest react-native-web

aws-amplify-react-native@4.2.1 (latest) depends on react-native-elements@0.19.1 which breaks using react-native-web @0.12.x or greater. react-native-elements@2.0.1 fixes the problem. Now we need an update of aws-amplify-react-native using react-native-elements@2.0.1 or later.

**Filed 3 bugs:**

<https://github.com/aws-amplify/amplify-js/issues/5957>

Closed - <https://github.com/aws-amplify/amplify-js/issues/5865>

Closed - <https://github.com/react-native-elements/react-native-elements/issues/2368>

## Broken using "react-native-web": "~0.13.1"

`Failed to compile D:/dev0/amplify-experiment/expo-amplify/node_modules/react-native-elements/src/config/ViewPropTypes.js Module not found: Can't resolve 'react-native-web/dist/exports/ViewPropTypes' in 'D:\dev0\amplify-experiment\expo-amplify\node_modules\react-native-elements\src\config'`

## Works using "react-native-web": "~0.11.7"

See reason: <https://github.com/necolas/react-native-web/releases/tag/0.12.0>

Short answer: 0.12.x removed use of the prop types exports which have been deprecated in React Native.

## Workaround - not tested beyond the trivial fix

Thanks to [Nick Sweet](https://github.com/aws-amplify/amplify-js/issues/5957#issuecomment-652546708), there appears to be a workaround. I'll test it on non-trivial examples ...

```
"aws-amplify-react-native": {
      "version": "4.2.1",
      "resolved": "https://registry.npmjs.org/aws-amplify-react-native/-/aws-amplify-react-native-4.2.1.tgz",
      "integrity": "sha512-J08OL5f8irWPDYbcgUYTS/cmNBBmHgf4hpmNvqGDJdcXpSIbnRR+nFQQXDVkvyJ5UJQnfgMpUXpBEASfSMBUow==",
      "requires": {
        "babel-preset-es2015": "^6.24.1",
        "buffer": "^5.2.1",
        "react-native-elements": "^2.0.4",
        "react-native-vector-icons": "^6.6.0"
      },
      "dependencies": {
        "buffer": {
          "version": "5.6.0",
          "resolved": "https://registry.npmjs.org/buffer/-/buffer-5.6.0.tgz",
          "integrity": "sha512-/gDYp/UtU0eA1ys8bOs9J6a+E/KWIY+DZ+Q2WESNUA0jFRsJOc0SNUO6xJ5SGA1xueg3NL65W6s+NY5l9cunuw==",
          "requires": {
            "base64-js": "^1.0.2",
            "ieee754": "^1.1.4"
          }
        },
        "react-native-elements": {
          "version": "2.0.4",
          "resolved": "https://registry.npmjs.org/react-native-elements/-/react-native-elements-2.0.4.tgz",
          "integrity": "sha512-nIFz47Sk/urOxZX+sqgWF2k7IVL0t9NGsVLg4HC7pN70bsjXMr4VUmS72zioxag3Du8xK1g7lw4vrRX3JQeVYg==",
          "requires": {
            "@types/react-native-vector-icons": "^6.4.5",
            "color": "^3.1.0",
            "deepmerge": "^3.1.0",
            "hoist-non-react-statics": "^3.1.0",
            "lodash.isequal": "^4.5.0",
            "opencollective-postinstall": "^2.0.0",
            "prop-types": "^15.7.2",
            "react-native-ratings": "^7.2.0",
            "react-native-status-bar-height": "^2.5.0"
          }
        }
      }
    },
```

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
