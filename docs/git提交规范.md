# git 提交规范

对于 git 提交规范 来说，不同的团队可能会有不同的标准，就以目前使用较多的 Angular团队规范 延伸出的 Conventional Commits specification（约定式提交） 为例，详解 git 提交规范。

约定式提交规范要求如下：

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]

--------  翻译 -------------
    
<类型>[可选 范围]: <描述>

[可选 正文]

[可选 脚注]
```

其中 <type> 类型，必须是一个可选的值，比如：

新功能：feat
修复：fix
文档变更：docs
…

也就是说，如果要按照 约定式提交规范 来去做的化，那么你的一次提交描述应该式这个样子的：

[git](images/1.png)

## Commitizen 规范化提交代码

commitizen 仓库名为 cz-cli ，它提供了一个 git cz 的指令用于代替 git commit，简单一句话介绍它：

> 当你使用 commitizen 进行代码提交（git commit）时，commitizen 会提交你在提交时填写所有必需的提交字段！

1. 全局安装 Commitizen

```bash
npm install commitizen@4.2.4 -g
```

2. 安装并配置 cz-customizable 插件

```bash
npm i cz-customizable@6.3.0 -D
```

添加以下配置到 package.json 中

```
...
  "config": {
    "commitizen": {
      "path": "node_modules/cz-customizable"
    }
  }
```

3. 项目根目录下创建 .cz-config.js 自定义提示文件

```js
module.exports = {
  // 可选类型
  types: [
    { value: 'feat', name: 'feat:     新功能' },
    { value: 'fix', name: 'fix:      修复' },
    { value: 'docs', name: 'docs:     文档变更' },
    { value: 'style', name: 'style:    代码格式(不影响代码运行的变动)' },
    {
      value: 'refactor',
      name: 'refactor: 重构(既不是增加feature，也不是修复bug)'
    },
    { value: 'perf', name: 'perf:     性能优化' },
    { value: 'test', name: 'test:     增加测试' },
    { value: 'chore', name: 'chore:    构建过程或辅助工具的变动' },
    { value: 'revert', name: 'revert:   回退' },
    { value: 'build', name: 'build:    打包' }
  ],
  // 消息步骤
  messages: {
    type: '请选择提交类型:',
    customScope: '请输入修改范围(可选):',
    subject: '请简要描述提交(必填):',
    body: '请输入详细描述(可选):',
    footer: '请输入要关闭的issue(可选):',
    confirmCommit: '确认使用以上信息提交？(y/n)'
  },
  // 跳过问题
  skipQuestions: ['body', 'footer'],
  // subject文字长度默认是72
  subjectLimit: 72
}
```

4. 使用 git cz 代替 git commit

使用 git cz 代替 git commit，即可看到提示内容。

但是当前依然存在着一个问题，那就是我们必须要通过 git cz 指令才可以完成规范化提交！

那么如果有马虎的同事，它们忘记了使用 git cz 指令，直接就提交了怎么办呢？

那么有没有方式来限制这种错误的出现呢？