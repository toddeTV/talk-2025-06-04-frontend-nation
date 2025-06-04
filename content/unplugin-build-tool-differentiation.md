---
layout: basic
---

# unplugin differentiate between build tools

1. Via build tool plugin files
2. In your plugin code, e.g.:

````md magic-move {lines: true}
```ts {*}
let _isBuild = true
export function isBuild(): boolean { return _isBuild }
export const buildDetector: UnpluginFactory<Options, false> = () => ({
  esbuild: {
    // No way to detect build/serve mode.
  },
  farm: {
    configureDevServer() {
      _isBuild = false
    },
  },
  rolldown: {}, // Has only build mode.
  rollup: {}, // Has only build mode.
  rspack(compiler) { detectWebpackDevServer(compiler) },
  vite: {
    configResolved(config) {
      _isBuild = config.command === 'build'
    },
  },
  webpack(compiler) { detectWebpackDevServer(compiler) },
})
```
````
