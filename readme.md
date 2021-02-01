# webpack5 + typescript + react 项目

- webpack5 不配置 webpack.config.dev.js 和 webpack.config.prd.js ,通过 process.env 来判断

# 初始化项目

```
cd typescript-react-project && npm init -y
```

# 创建 webpack.config.js 打包文件

# 支持 typescript 语法-需要生成一个 tsconfig.json 文件来告诉 ts-loader 如何编译代码 TypeScript 代码

- 生成 tsconfig.json 文件，运行 tsc --init 命令

```
{
  "compilerOptions": {
    "moduleResolution":"Node",
    "outDir": "./dist",
    "sourceMap": true,
    "noImplicitAny": true, //不能包含ts中的any类型
    "module": "ESNext",
    "target": "es5",
    "jsx": "react",
    "esModuleInterop":true,
    "baseUrl": ".",  // 解析非相对模块的基地址，默认是当前目录
    "paths": {       // 路径映射，相对于baseUrl
      "@/*": ["./src/*" ] //把@映射为src目录
    }
  },
  "include": [
    "./src/**/*"
  ]
}
```

# 生成和配置 eslint 的配置文件.eslintrc.js

- 在终端运行 npx eslint --init 命令 生成 .eslintrc.js 或者.eslintrc.json 配置文件, 命令并根据提示一路安装 eslint-plugin-react@latest @typescript-eslint/eslint-plugin@latest @typescript-eslint/parser@latest
- ✔ How would you like to use ESLint? · problems
- ✔ What type of modules does your project use? · esm
- ✔ Which framework does your project use? · react
- ✔ Does your project use TypeScript? · No / Yes
- ✔ Where does your code run? · browser
- ✔ What format do you want your config file to be in? · JavaScript or JSON
- Warning: React version not specified in eslint-plugin-react settings. See https://github.com/yannickcr/eslint-plugin-react#configuration .

# 在 vscode 配置自动修复

- 安装 vscode 的 eslint 插件
- 配置参数 .vscode\settings.json

```setting.json
{
 "eslint.autoFixOnSave": true,
 "eslint.validate": [
     "javascript",
     "javascriptreact",
     {
         "language": "typescript",
         "autoFix": true
     },
      {
         "language": "typescriptreact",
         "autoFix": true
     }
 ]
}
```

# 配置 Git Hooks 检查，规范提交日志

## 安装 husky

- 可以通过项目根目录中执行 git init 命令，查看 git 的所有 hooks
- 安装 husky，安装 husky 之后，可以看到 .git/hooks 目录中文件的变化

```
npm i husky --save-dev
```

- 全局或局部安装 commitizen,全局安装可以用 git cz 代替 git commit

```
npm i -g commitizen

```

## 安装 cz-conventional-changelog

- cz-conventional-changelog 是一个 commitizen 的 adapter，它实现的是 conventional-changelog-angular 一套业界公认和常用的 convention
- commit-message-format

```
npm i cz-conventional-changelog -D
```

## 安装 commitlint

- commitlint 用来在代码提交前来校验我们的代码是否符合标准
- commitlint 也需要个 adapter @commitlint/config-conventional

```
npm i @commitlint/config-conventional @commitlint/cli  --save-dev
```

- 生成变更日志：conventional-changelog-cli

```
npm i -g conventional-changelog-cli
```

- 生成最新的日志

```
conventional-changelog -p angular -i CHANGELOG.md -s
```

- 代码格式化:lint-staged 在每个团队成员提交的时候，只检查当次改动的文件

```
npm i  lint-staged --save-dev
```
