## Setup

```
npm run eject
```

## Find css-loader

Change in webpack.config.dev.js, options

```javascript
modules: true,
localIdentName: "[name]__[local]__[hash:base64:5]",
```

Change in webpack.config.prod.js, options

```javascript
modules: true,
localIdentName: "[name]__[local]__[hash:base64:5]",
```
