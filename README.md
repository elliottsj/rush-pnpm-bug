# rush-pnpm-bug

Reproduction of a bug with Rush + pnpm: https://github.com/Microsoft/web-build-tools/issues/1142

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

**This bug seems not to occur when using pnpm without Rush**. I've copied `common/temp/package.json` and `common/config/rush/shrinkwrap.yaml` into a directory `pnpm-only/` and removed all references to "mypackage.tgz". Perform the install using just pnpm:

```shell
$ cd pnpm-only/
$ npm install --global pnpm@2.25.6
$ pnpm install
$ cat node_modules/.registry.npmjs.org/react-focus-lock/1.17.7/node_modules/react-focus-lock/package.json
{
  "name": "react-focus-lock",
  "version": "1.17.7",
  "description": "It is a trap! (for a focus)",
  ...
```

This may indicate that it's actually a pnpm bug related to `.tgz` dependencies?
