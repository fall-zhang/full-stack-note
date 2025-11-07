> Create by **fall** on 03 Nov 2025<br/>
> Recently revised in 03 Nov 2025

官方文档

https://github.com/golang/vscode-go/wiki/settings#settings-for-gopls

项目过大的时候，gopls 项目占用动辄 90%，占用内存，动辄 4G。使用以下 vscode 配置，可以优化这种情况：

```json
{
  // go Conf
  "go.useLanguageServer": true,
  "go.languageServerFlags": [
    //   "--enable-semantic-tokens", // 启用语法高亮增强
    "-rpc.trace" // 开启 RPC 调用追踪，用于分析性能瓶颈。
  ],
  "gopls": {
    "build.env": {
      "GOMAXPROCS": "5"
    },
    "directoryFilters": [
      "-**/node_modules",
      "-**/vendor",
      "-**/build",
      "-**/dist",
      "-**/.git"
    ],
    // "diagnosticsTrigger": "Save", // 将诊断触发时机从`实时`(默认)改为`保存时`
    "usePlaceholders": true, // 函数补全时提供参数占位符
    "ui.semanticTokens": true,
    "ui.documentation.linksInHover": "gopls",
    "completeUnimported": true,
    "deepCompletion": true, // 启用深层补全，提供更全面的代码建议
    // "build.expandWorkspaceToModule": false, // 打开工作区文件夹时，减少工作来使工作区保持最新
    "expandWorkspaceToModule": false,
    // Go: Restart Language Server 命令。这能清除 gopls 的当前状态，通常能解决因内存累积或状态异常导致的瞬时高 CPU 问题。
    "analyses": {
      "unusedparams": true, // 提示未使用的参数
      "unusedwrite": true, // 检查未使用的赋值
      "shadow": true, // 检查未使用的赋值
      // 如果项目庞大，可以考虑关闭以下检查以提升性能
      "fieldalignment": false,
      "nilness": false
    },
    // 如果性能开销还是高，禁用部分高开销的静态分析
    // 关闭完整的 staticcheck 分析套件
    "staticcheck": false,
    // 按需禁用部分代码透镜
    "codelenses": {
      "generate": false,
      "upgrade_dependency": false
    }
  },
  "[go]": {
    // "editor.defaultFormatter": "golang.go",
    "editor.formatOnSave": false,
    "editor.snippetSuggestions": false,
    "editor.codeActionsOnSave": {
      "source.organizeImports": "never"
    },
    "editor.defaultFormatter": "golang.go",
  },
}
```

