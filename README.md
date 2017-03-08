# node.js中的相关测试
### 主要介绍关于node.js中的代码规范测试，模块测试，功能测试等问题
===============
## ESLint
1 学会使用 ESLint 进行代码检查。
## 操作步骤
（1）进入demos/eslint-demo目录，安装 ESLint。<br>
`$ cd demos/eslint-demo`<br>
`$ npm install eslint --save-dev`<br>
（2）通常，我们会使用别人已经写好的代码检查规则，这里使用的是 Airbnb 公司的规则。所以，还要安装 ESLint 这个规则模块。<br>
`$ npm install eslint-plugin-import eslint-config-airbnb-base --save-dev`<br>
上面代码中，eslint-plugin-import是运行这个规则集必须的，所以也要一起安装。<br>
（3）ESLint 的配置文件是.eslintrc.json，放置在项目的根目录下面。新建这个文件，在里面指定使用 Airbnb 的规则。<br>
```
{
  "extends": "airbnb-base"
}
```
（4）打开项目的package.json，在scripts字段里面添加三个脚本。<br>
```
{
  // ...
  "scripts" : {
    "test": "echo \"Error: no test specified\" && exit 1",
    "lint": "eslint **/*.js",
    "lint-html": "eslint **/*.js -f html -o ./reports/lint-results.html",
    "lint-fix": "eslint --fix **/*.js"
  },
  // ...
}
```
