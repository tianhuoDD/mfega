# 项目介绍

> **OpusMart**：“Opus”（作品、杰作）和“Mart”（市场）。这个名字寓意着商场是一个精品杰作的集合地，提供精致、独特的商品，适合文化艺术品类或者精心策划的高端商城。

项目使用`monorepo`架构：

- `apps`：存放项目
- `packages`：存放组件
- `libs`：存放工具

`monorepo`架构依赖：esLint v9.15.0 + prettier v3.4.0 + lint-staged v15.2.10 + husky v9.1.7 + cz-git v1.11.0 + commitizen v4.3.1

# 开发指南

> **安装依赖时，必须明确是 _开发环境_ 依赖、还是 _生产环境_ 依赖**

## 使用的依赖/包/扩展

### 开发环境依赖

1. 代码格式化相关：`@eslint/js`、`eslint`、`eslint-plugin-vue`、`globals`、`prettier`、`eslint-plugin-prettier`、`eslint-config-prettier`
2. git相关：`husky`、`lint-staged`、`@commitlint/{cli,config-conventional}`

### 使用的VS Code扩展

1. ESLint
2. Prettier - Code formatter
3. EditorConfig for VS Code
4. JSONComments

## shell命令相关


### 开发相关命令

1. 初始化依赖

   ```shell
   pnpm i
   ```

2. 启动服务

   ```shell
   pnpm -F=app run dev
   # or
   pnpm run om
   ```

3. 添加依赖

   ```shell
   # -P是生产环境、-D是开发环境
   pnpm -F=app add -P <package>
   pnpm -F=app add -D <package>

   # 向工作区根目录添加依赖
   pnpm add -D <package> -w
   ```

### 包管理器相关命令

1. 升级node

   > 使用nvm的情况可直接使用命令，否则需要手动下载安装

   ```shell
   nvm install v20.15.0
   nvm use v20.15.0
   ```

2. 安装pnpm

   ```shell
   npm install -g pnpm@9.14.2
   ```

3. 在该项目中，我通过限制npm的版本，来达到了无法使用npm的目的，以统一使用pnpm，避免项目管理混乱

### git相关命令

1. 提交规范: `<type>(<scope>): <subject>`
   | type | 描述 |
   | ----------- | ----------- |
   | `feat` | 新增功能 |
   | `fix` | 修复bug |
   | `docs` | 文档变更 |
   | `style` | 代码格式优化 |
   | `refactor` | 代码重构 |
   | `perf` | 性能优化 |
   | `test` | 对测试的改动 |
   | `build` | 依赖的变更 |
   | `ci` | 修改 CI 配置 |
   | `revert` | 回滚 commit |
   | `chore` | 对辅助工具和库的更改 |

   **注意点:** type和subject间的冒号是英文半角，且后面 **衔接空格** 。示例：`<type>`+`:`+` `+`<subject>`

2. git-cz快捷命令：
   ```shell
   # 需先全局安装 commitizen
   pnpm i -g commitizen
   # 在终端中运行(法一)
   git cz
   # (法二)
   cz
   # (法三)
   pnpm run commit
   ```
3. 回退版本 - **请使用revert回退版本**，避免发生无可挽回的错误
   ```shell
   # 回退指定版本(留下记录)
   git revert <版本号>
   # 终止回退版本
   git revert --abort
   ```

# 可能遇到的问题

1. Cannot destructure property 'manifest' of 'manifestsByPath[rootDir]' as it is undefined.
   该问题出现在：`pnpm add xxx`时。这是因为pnpm无法找到安装目录。
   解决方法：请使用`pnpm -F="opus-mart" add xxx`或`pnpm add xxx -w`来[指定工作目录](#开发相关命令)。（此问题仅出现在monorepo架构，具体解决方案可查看：https://github.com/pnpm/pnpm/issues/6524）
2. .husky/pre-commit: .husky/pre-commit: cannot execute binary file
   该问题出现原因是：`.husky`的`pre-commit`文件编码为`utf-16`，导致文件无法被解码。
   解决方法：将`pre-commit`文件编码改为`utf-8`即可。（此问题可能源于`husky init`命令，自动生成的文件编码不正确，具体解决方案可查看：https://stackoverflow.com/questions/77364609/cannot-execute-binary-file-exec-format-error-code-126）
3. git提交时提示：`Git:vexios@1.0.1 lint:lint-staged E:\VS Code\Project\VEXIOS`
   该问题出现的原因是：你没有安装要求的提交规范编写msg，具体可点击`显示命令输出`按钮查看
   解决方法：请按照提示[修改msg](#git相关命令)，~~ 或者使用`git commit --no-verify`绕过检查。~~

## 项目开发中的问题

1. Rom遇到的问题会使用`@rom:error`来标记，以便快速查找

# 展望

1. 可添加的依赖: `@antfu/eslint-config`、`stylelint`、`lodash-es`、
2. 可以使用的技术: `vueUse`、`turbo`、[`rimraf`](https://github.com/isaacs/rimraf)、[`del`](https://www.npmjs.com/package/del)、`consola`、`rollup-plugin-visualizer`
3. 可使用的语言: `typescript`

