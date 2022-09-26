<details open="" style="box-sizing: border-box; display: block; margin-top: 0px; margin-bottom: 16px;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer;">Rollup</summary><slot id="details-content"><br style="box-sizing: border-box;"><div class="highlight highlight-source-ts notranslate position-relative overflow-auto" dir="auto" style="box-sizing: border-box; position: relative !important; overflow: auto !important; margin-bottom: 16px;"><pre style="box-sizing: border-box; font-family: ui-monospace, SFMono-Regular, &quot;SF Mono&quot;, Menlo, Consolas, &quot;Liberation Mono&quot;, monospace; font-size: 13.6px; margin-top: 0px; margin-bottom: 0px; overflow-wrap: normal; padding: 16px; overflow: auto; line-height: 1.45; background-color: var(--color-canvas-subtle); border-radius: 6px; word-break: normal;"><span class="pl-c" style="box-sizing: border-box; color: var(--color-prettylights-syntax-comment);">// rollup.config.js</span>
<span class="pl-k" style="box-sizing: border-box; color: var(--color-prettylights-syntax-keyword);">import</span> <span class="pl-smi" style="box-sizing: border-box; color: var(--color-prettylights-syntax-storage-modifier-import);">AutoImport</span> <span class="pl-k" style="box-sizing: border-box; color: var(--color-prettylights-syntax-keyword);">from</span> <span class="pl-s" style="box-sizing: border-box; color: var(--color-prettylights-syntax-string);">'unplugin-auto-import/rollup'</span>

<span class="pl-k" style="box-sizing: border-box; color: var(--color-prettylights-syntax-keyword);">export</span> <span class="pl-k" style="box-sizing: border-box; color: var(--color-prettylights-syntax-keyword);">default</span> <span class="pl-kos" style="box-sizing: border-box;">{</span>
  <span class="pl-c1" style="box-sizing: border-box; color: var(--color-prettylights-syntax-constant);">plugins</span>: <span class="pl-kos" style="box-sizing: border-box;">[</span>
    <span class="pl-smi" style="box-sizing: border-box; color: var(--color-prettylights-syntax-storage-modifier-import);">AutoImport</span><span class="pl-kos" style="box-sizing: border-box;">(</span><span class="pl-kos" style="box-sizing: border-box;">{</span> <span class="pl-c" style="box-sizing: border-box; color: var(--color-prettylights-syntax-comment);">/* options */</span> <span class="pl-kos" style="box-sizing: border-box;">}</span><span class="pl-kos" style="box-sizing: border-box;">)</span><span class="pl-kos" style="box-sizing: border-box;">,</span>
    <span class="pl-c" style="box-sizing: border-box; color: var(--color-prettylights-syntax-comment);">// other plugins</span>
  <span class="pl-kos" style="box-sizing: border-box;">]</span><span class="pl-kos" style="box-sizing: border-box;">,</span>
<span class="pl-kos" style="box-sizing: border-box;">}</span></pre></div><p dir="auto" style="box-sizing: border-box; margin-top: 0px; margin-bottom: 16px;"><br style="box-sizing: border-box;"></p></slot></details>



<details style="box-sizing: border-box; display: block; margin-top: 0px; margin-bottom: 16px;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer;">Webpack</summary></details>



<details style="box-sizing: border-box; display: block; margin-top: 0px; margin-bottom: 16px;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer;">Nuxt</summary></details>



<details style="box-sizing: border-box; display: block; margin-top: 0px; margin-bottom: 16px;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer;">Vue CLI</summary></details>



<details style="box-sizing: border-box; display: block; margin-top: 0px; margin-bottom: 16px;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer;">Quasar</summary></details>



<details style="box-sizing: border-box; display: block; margin-top: 0px; margin-bottom: 16px;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer;">esbuild</summary></details>



## Configuration

```
AutoImport({
  // targets to transform
  include: [
    /\.[tj]sx?$/, // .ts, .tsx, .js, .jsx
    /\.vue$/, /\.vue\?vue/, // .vue
    /\.md$/, // .md
  ],

  // global imports to register
  imports: [
    // presets
    'vue',
    'vue-router',
    // custom
    {
      '@vueuse/core': [
        // named imports
        'useMouse', // import { useMouse } from '@vueuse/core',
        // alias
        ['useFetch', 'useMyFetch'], // import { useFetch as useMyFetch } from '@vueuse/core',
      ],
      'axios': [
        // default imports
        ['default', 'axios'], // import { default as axios } from 'axios',
      ],
      '[package-name]': [
        '[import-names]',
        // alias
        ['[from]', '[alias]'],
      ],
    },
  ],

  // Auto import for module exports under directories
  // by default it only scan one level of modules under the directory
  dirs: [
    // './hooks',
    // './composables' // only root modules
    // './composables/**', // all nested modules
    // ...
  ],

  // Filepath to generate corresponding .d.ts file.
  // Defaults to './auto-imports.d.ts' when `typescript` is installed locally.
  // Set `false` to disable.
  dts: './auto-imports.d.ts',

  // Auto import inside Vue template
  // see https://github.com/unjs/unimport/pull/15 and https://github.com/unjs/unimport/pull/72
  vueTemplate: false,

  // Custom resolvers, compatible with `unplugin-vue-components`
  // see https://github.com/antfu/unplugin-auto-import/pull/23/
  resolvers: [
    /* ... */
  ],

  // Generate corresponding .eslintrc-auto-import.json file.
  // eslint globals Docs - https://eslint.org/docs/user-guide/configuring/language-options#specifying-globals
  eslintrc: {
    enabled: false, // Default `false`
    filepath: './.eslintrc-auto-import.json', // Default `./.eslintrc-auto-import.json`
    globalsPropValue: true, // Default `true`, (true | false | 'readonly' | 'readable' | 'writable' | 'writeable')
  },
})
```

Refer to the [type definitions](https://github.com/antfu/unplugin-auto-import/blob/main/src/types.ts) for more options.

## Presets

See [src/presets](https://github.com/antfu/unplugin-auto-import/blob/main/src/presets).

## TypeScript

In order to properly hint types for auto-imported APIs

| Enable `options.dts` so that `auto-imports.d.ts` file is automatically generatedMake sure `auto-imports.d.ts` is not excluded in `tsconfig.json` | `AutoImport({  dts: true // or a custom path })` |
| ------------------------------------------------------------ | ------------------------------------------------ |
|                                                              |                                                  |

## ESLint

> 💡 When using TypeScript, we recommend to **disable** `no-undef` rule directly as TypeScript already check for them and you don't need to worry about this.

If you have encountered ESLint error of `no-undef`:

| Enable `eslintrc.enabled` | `AutoImport({  eslintrc: {    enabled: true, // <-- this  }, })` |
| ------------------------- | ------------------------------------------------------------ |
|                           |                                                              |

| Update your `eslintrc`: [Extending Configuration Files](https://eslint.org/docs/user-guide/configuring/configuration-files#extending-configuration-files) | `// .eslintrc.js module.exports = {  extends: [    './.eslintrc-auto-import.json',  ], }` |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

## FAQ

### Compare to [`unimport`](https://github.com/unjs/unimport)

From v0.8.0, `unplugin-auto-import` **uses** `unimport` underneath. `unimport` is designed to be a lower level tool (it also powered Nuxt's auto import). You can think `unplugin-auto-import` is a wrapper of it that provides more user-friendly config APIs and capability like resolvers. Development of new features will mostly happend in `unimport` from now.

### Compare to [`vue-global-api`](https://github.com/antfu/vue-global-api)

You can think of this plugin as a successor to `vue-global-api`, but offering much more flexibility and bindings with libraries other than Vue (e.g. React).

###### Pros

- Flexible and customizable
- Tree-shakable (on-demand transforming)
- No global population

###### Cons

- Relying on build tools integrations (while `vue-global-api` is pure runtime) - but hey, we have supported quite a few of them already!

## Sponsors

[![img](https://camo.githubusercontent.com/a3f2588858b3087ad2a416ca3d8b2e6e41993dfd471fd44e97850cf95a91fd3a/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f616e7466752f7374617469632f73706f6e736f72732e737667)](https://cdn.jsdelivr.net/gh/antfu/static/sponsors.svg)

## License

[MIT](https://github.com/antfu/unplugin-auto-import/blob/main/LICENSE) License © 2021 [Anthony Fu](https://github.com/antfu)

## About

Auto import APIs on-demand for Vite, Webpack and Rollup

### Topics

[webpack-plugin](https://github.com/topics/webpack-plugin) [rollup-plugin](https://github.com/topics/rollup-plugin) [vite-plugin](https://github.com/topics/vite-plugin) [unplugin](https://github.com/topics/unplugin)

### Resources

[ Readme](https://github.com/antfu/unplugin-auto-import#readme)

### License

[ MIT license](https://github.com/antfu/unplugin-auto-import/blob/main/LICENSE)

### Code of conduct

[ Code of conduct](https://github.com/antfu/.github/blob/main/CODE_OF_CONDUCT.md)



### Stars

[ **1.4k** stars](https://github.com/antfu/unplugin-auto-import/stargazers)

### Watchers

[ **8** watching](https://github.com/antfu/unplugin-auto-import/watchers)

### Forks

[ **101** forks](https://github.com/antfu/unplugin-auto-import/network/members)

## [Releases 84](https://github.com/antfu/unplugin-auto-import/releases)

[v0.11.2Lateston 18 Aug](https://github.com/antfu/unplugin-auto-import/releases/tag/v0.11.2)

[+ 83 releases](https://github.com/antfu/unplugin-auto-import/releases)

## Sponsor this project

[![@antfu](https://avatars.githubusercontent.com/u/11247099?s=64&v=4)](https://github.com/antfu)[**antfu** Anthony Fu](https://github.com/antfu)

[ Sponsor](https://github.com/sponsors/antfu)

[Learn more about GitHub Sponsors](https://github.com/sponsors)

## [Packages](https://github.com/users/antfu/packages?repo_name=unplugin-auto-import)

No packages published

## [Contributors 39](https://github.com/antfu/unplugin-auto-import/graphs/contributors)

- [![@antfu](https://avatars.githubusercontent.com/u/11247099?s=64&v=4)](https://github.com/antfu)
- [![@userquin](https://avatars.githubusercontent.com/u/6311119?s=64&v=4)](https://github.com/userquin)
- [![@sxzz](https://avatars.githubusercontent.com/u/6481596?s=64&v=4)](https://github.com/sxzz)
- [![@Jungzl](https://avatars.githubusercontent.com/u/35426360?s=64&v=4)](https://github.com/Jungzl)
- [![@Demivan](https://avatars.githubusercontent.com/u/2339406?s=64&v=4)](https://github.com/Demivan)
- [![@dammy001](https://avatars.githubusercontent.com/u/30652791?s=64&v=4)](https://github.com/dammy001)
- [![@JounQin](https://avatars.githubusercontent.com/u/8336744?s=64&v=4)](https://github.com/JounQin)
- [![@Weilence](https://avatars.githubusercontent.com/u/11787429?s=64&v=4)](https://github.com/Weilence)
- [![@sibbng](https://avatars.githubusercontent.com/u/19991745?s=64&v=4)](https://github.com/sibbng)
- [![@tdolsen](https://avatars.githubusercontent.com/u/180510?s=64&v=4)](https://github.com/tdolsen)
- [![@jfgodoy](https://avatars.githubusercontent.com/u/731635?s=64&v=4)](https://github.com/jfgodoy)

[+ 28 contributors](https://github.com/antfu/unplugin-auto-import/graphs/contributors)

## Languages

- [TypeScript96.8%](https://github.com/antfu/unplugin-auto-import/search?l=typescript) 
- [Vue2.4%](https://github.com/antfu/unplugin-auto-import/search?l=vue) 
- [HTML0.8%](https://github.com/antfu/unplugin-auto-import/search?l=html)

## Footer

© 2022 GitHub, Inc.

Footer navigation[Terms](https://docs.github.com/en/github/site-policy/github-terms-of-service)[Privacy](https://docs.github.com/en/github/site-policy/github-privacy-statement)[Security](https://github.com/security)[Status](https://www.githubstatus.com/)[Docs](https://docs.github.com/)[Contact GitHub](https://support.github.com/?tags=dotcom-footer)[Pricing](https://github.com/pricing)[API](https://docs.github.com/)[Training](https://services.github.com/)[Blog](https://github.blog/)[About](https://github.com/about)