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
除了原有的test脚本，上面代码新定义了三个脚本，它们的作用如下。<br>
* lint：检查所有js文件的代码
* lint-html：将检查结果写入一个网页文件./reports/lint-results.html
* lint-fix：自动修正某些不规范的代码
（5）运行静态检查命令。<br>
```
$ npm run lint

  1:5  error    Unexpected var, use let or const instead  no-var
  2:5  warning  Unexpected console statement              no-console

✖ 2 problems (1 error, 1 warning)
```
正常情况下，该命令会从index.js脚本里面，检查出来两个错误：一个是不应该使用var命令，另一个是不应该在生产环境使用console.log方法。<br>
（6）修正错误。<br>
`$ npm run lint-fix`
运行上面的命令以后，再查看index.js，可以看到var x = 1;被自动改成了const x = 1;。这样就消除了一个错误，但是还留下一个错误。<br>
（7）修改规则。<br>
由于我们想要允许使用console.log方法，因此可以修改.eslintrc.json，改变no-console规则。请将.eslintrc.json改成下面的样子。<br>
```
{
  "extends": "airbnb-base",

  "rules": {
    "no-console": "off"
  }
  ```
  再运行npm run lint，就不会报错了。<br>
  `$ npm run lint`
