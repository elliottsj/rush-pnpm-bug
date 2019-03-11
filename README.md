# rush-pnpm-bug

Reproduction of a bug with Rush + pnpm.

The bug is that **react-focus-lock@1.18.2** is installed, despite **react-focus-lock@1.17.7** being declared in [shrinkwrap.yaml](common/config/rush/shrinkwrap.yaml):

```shell
$ npm install --global @microsoft/rush
$ rush install
$ cat common/temp/node_modules/.registry.npmjs.org/react-focus-lock/1.18.2/react@16.8.3/node_modules/react-focus-lock/package.json
{
  "name": "react-focus-lock",
  "version": "1.18.2",
  "description": "It is a trap! (for a focus)",
  ...
```
