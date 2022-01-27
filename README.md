
### Docusaurus blog-only Tutorial

https://blog.alanwei.com/docs/guides/blog

Summary:

update presets without landing page:

```js
// docusaurus.config.js

module.exports = {
  // ...
  presets: [
    [
      '@docusaurus/preset-classic',
      {
        docs: false,
        blog: {
          path: './blog',
          routeBasePath: '/', // Set this value to '/'.
        },
      },
    ],
  ],
};
```
- delete or rename file `./src/pages/index.js`