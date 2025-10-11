---
sidebar_position: 3
---

> Create by **fall** on 06 Feb 2021<br/>
> Recently revised in 26 Sep 2025

## TS 配置

初始化开发环境

```bash
tsc --init // 初始化开发环境
# tsc 是 typescript 的检查命令
```

ts 项目中，根目录下面的 tsconfig.json 是配置文件，如果文件是一个空的 json 文件

TypeScript 将会把此目录和子目录下的所有 .ts 文件作为编译上下文的一部分，它还会包含一部分默认的编译选项。

### 环境配置

对于不同的环境，可能需要不同的 TypeScript 文件进行配置，因此可能需要多个配置文件

- `tsconfig.json`：vscode、`tsc` 命令默认读取的配置
- `tsconfig.base.json`：基础配置
- `tsconfig.node.json`：node 环境配置

当然，你可以自定义其它名称的配置

可以在运行环境检查时，指定对应的配置文件

```bash
tsc -p tsconfig.build.json
# 指定 tsconfig.build.json 作为类型检查的文件
```

### 指定文件

好的 IDE 支持对 TypeScript 的即时编译

> VS Code 中，终端 -> 运行任务 -> typescript -> 监视

指定文件

```json
{
  "files":['./some/file.ts'], // 指定需要编译的文件
  // include 和 exclude 选项用来指定需要包含的文件和排除的文件
	"include":[
    "./folder",
    "src/**/*.ts",
    "src/**/*.tsx"
  ],
  "exclude":[
    "node_modules"
  ]
}
```

## 常用配置

### exactOptionalPropertyTypes

只允许初始化时不赋值，不允许再设置为空，

> 因为，未赋值和手动设置为 `undefined` 会导致 `in` 操作结果的不一致。

```ts
// 设置 exactOptionalPropertyTypes:true

interface UserDefaults {
  // The absence of a value represents 'system'
  colorThemeOverride?: 'dark' | 'light';
}

const settings:UserDefaults = {
  colorThemeOverride: undefined
}
settings.colorThemeOverride = 'dark'
settings.colorThemeOverride = 'light'

// But not:
settings.colorThemeOverride = undefined
```

### 字段配置详情

```json
{
  // 引入其他配置文件，继承配置(把基础配置抽离成tsconfig.base.json文件，然后引入)
  "extends": "./tsconfig.base.json",
  // 指定一个匹配列表，支持 glob 通配符（属于自动指定该路径下的所有ts相关文件）
  "include": [
    "src/**/*"
  ],
  // 指定一个排除列表，支持 glob 通配符（include的反向操作）
  "exclude": [
    "demo.ts"
  ],
  // 指定哪些文件使用该配置（属于手动一个个指定文件）
  "files": [
    "demo.ts"
  ],
  // 指定工程引用依赖。
  "references": [
    {"path": "./common"}
  ],
  // 设置自动引入库类型定义文件(.d.ts)相关。
  // enable : 布尔类型，是否开启自动引入库类型定义文件(.d.ts)，默认为 false；
  // include : 数组类型，允许自动引入的库名，如：[“jquery”, “lodash”]；
  // exclude : 数组类型，排除的库名。
  "typeAcquisition": {
    "enable": false,
    "exclude": ["jquery"],
    "include": ["jest"]
  },
  // 设置保存文件的时候自动编译，但需要编译器支持。
  "compileOnSave": false, 
  // 配置编译选项，若 compilerOptions 属性被忽略，则编译器会使用默认值
  "compilerOptions": { 
    /* 基本选项 */
    "target": "es5",                       // 指定目标 ECMAScript 版本: 'ES3' (default), 'ES5', 'ES6'/'ES2015', 'ES2016', 'ES2017', or 'ESNEXT'
    "module": "commonjs",                  // 生成代码的模板标准，指定使用模块: 'commonjs', 'amd', 'system', 'umd' or 'es2015'
    "lib": [],                             // 指定要包含在编译中的库文件（TS 的声明文件库），可为 ['dom',"es6","DOM.Iterable"]es5 默认引用 dom、es5、scripthost，如需要使用es的高级版本特性，通常都需要配置，如es8的数组新特性需要引入"ES2019.Array"
    "allowJs": true,                       // 允许编译 javascript 文件
    "checkJs": true,                       // 报告 javascript 文件中的错误，通常与 checkJs 一起使用
    "jsx": "preserve",                     // 指定 jsx 代码的生成: 'preserve', 'react-native', or 'react'
    "skipLibCheck":false,                  // 跳过 node_module 中的 type 检查
    "sourceMap": true,                     // 生成相应的 '.map' 文件
    "outFile": "./",                       // 将输出文件合并为一个文件，将多个相互依赖的文件生成一个文件，可以用在AMD模块中，即开启时应设置"module": "AMD",
    "outDir": "./",                        // 指定输出目录
    "rootDir": "./",                       // 用来控制输出目录结构 --outDir，用于控制输出目录结构
    "removeComments": true,                // 删除编译后的所有的注释
    "noEmit": true,                        // 编译后不会生成任何 js 文件
    "importHelpers": true,                 // 从 tslib 导入辅助工具函数，文件必须是模块
    "isolatedModules": true,               // 将每个文件作为单独的模块 （与 'ts.transpileModule' 类似）如果使 用esbuild 来转译 TypeScript，应当设置为 true
    "esModuleInterop": true,               // 允许 export= 导出，由 import from 导入
    "allowUmdGlobalAccess": true,          // 允许在模块中全局变量的方式访问 umd 模块
    "resolveJsonModule": true,             // 是否允许直接导入 JSON 文件作为模块。

    /* 严格的类型检查选项 */
    "strict": true,                        // 启用所有严格类型检查选项
    "noImplicitAny": true,                 // 不允许隐式的 any 类型，在表达式和声明上有隐含的 any 类型时报错
    "strictNullChecks": true,              // 启用严格的 null 检查
    "noImplicitThis": true,                // 当 this 表达式值为 any 类型的时候，生成一个报错
    "alwaysStrict": true,                  // 以严格模式检查每个模块，并在每个文件里加入 'use strict'
    "strictFunctionTypes": true,           // 不允许函数参数双向协变
    "strictPropertyInitialization": true,  // 类的实例属性必须初始化
    "strictBindCallApply": true,           // 严格的bind/call/apply检查

    /* 额外的检查 */
    "noUnusedLocals": true,                // 有未使用的变量时，抛出错误
    "noUnusedParameters": true,            // 函数有未使用的参数时，抛出错误
    "noImplicitReturns": true,             // 函数有分支中没有返回值时，抛出错误
    "noFallthroughCasesInSwitch": true,    // 报告 switch 语句的 fallthrough 错误。（即，没有 break 语句后面不会执行）

    /* 模块解析选项 */
    "moduleResolution": "node",            // 选择模块解析策略，默认用 node 的解析策略，即相对的方式导入 'node' (Node.js) or 'classic' (TypeScript pre-1.6)
    "baseUrl": "./",                       // 用于解析非相对模块名称的基目录，默认是当前目录
    "paths": { // 路径映射，相对于 baseUrl
      // 如使用jq时不想使用默认版本，而需要手动指定版本，可进行如下配置
      "jquery": ["node_modules/jquery/dist/jquery.min.js"]
    },
    "rootDirs": [],                        // 将多个目录放在一个虚拟目录下，用于运行时，即编译后引入文件的位置可能发生变化，这也设置可以虚拟src和out在同一个目录下，不用再去改变路径也不会报错
    "typeRoots": [],                       // 包含类型声明的文件目录，默认 node_modules/@types
    "types": [],                           // 需要包含的类型声明文件名列表
    "allowSyntheticDefaultImports": true,  // 允许从没有设置默认导出的模块中默认导入。

    /* Source Map Options */
    "sourceRoot": "./",                    // 指定调试器应该找到 TypeScript 文件而不是源文件的位置
    "mapRoot": "./",                       // 指定调试器应该找到映射文件而不是生成文件的位置
    "inlineSourceMap": true,               // 生成 inline SourceMap 文件，而不是将 sourcemaps 生成不同的文件，inline SourceMap 会包含在生成的js文件中
    "inlineSources": true,                 // 将代码与 sourcemaps 生成到一个文件中，要求同时设置了 --inlineSourceMap 或 --sourceMap 属性

    /* 声明文件 */
    "declaration": true,                   // 生成相应的 '.d.ts' 声明文件
    "declarationDir": "./file",            // 指定生成声明文件存放目录
    "emitDeclarationOnly": true,           // 只生成声明文件，而不会生成 js 文件
     "declarationMap": true,               // 为声明文件生成sourceMap

    /* 其他选项 */
    "experimentalDecorators": true,        // 启用装饰器
    "emitDecoratorMetadata": true,         // 为装饰器提供元数据的支持
    "tsBuildInfoFile": "./buildFile",      // 增量编译文件的存储位置
    "incremental": true,                   // 增量编译，TS 编译器在第一次编译之后会生成一个存储编译信息的文件，第二次编译会在第一次的基础上进行增量编译，可以提高编译的速度
    "diagnostics": true,                   // 打印诊断信息
     "noEmitOnError": true,                // 发送错误时不输出任何文件
    "downlevelIteration": true,            // 降级遍历器实现，如果目标源是 es3/5，那么遍历器会有降级的实现
    "noEmitHelpers": true,                 // 不生成helper函数，减小体积，需要额外安装，常配合importHelpers一起使用
    "listEmittedFiles": true,              // 打印输出文件
    "listFiles": true                      // 打印编译的文件(包括引用的声明文件)
  }
}
```



## 参考文章

| 名称               | 链接                                              |
| ------------------ | ------------------------------------------------- |
| 深入理解TypeScript | https://jkchao.github.io/typescript-book-chinese/ |



