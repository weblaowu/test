### 单元测试
- 测试包含单元测试，性能测试，安全测试和功能测试等几个方面。单元测试主要包含断言，测试框架，测试用例，测试覆盖率，mock, 持续集成等几个方面。

单元测试是什么？
- 对于前端开发来说，为了检测特定的代码是否达到预期的运行结果而采用专门的工具或方法来验证，并最终得到特定的结果。这样方便问题的排查和后期的修正。

为什么需要单元测试？
- 首先一个前端单元测试的原因是，JS是动态语言，缺少类型检查，编译期间无法定位到错误。
- 单元测试可以检测代码的正确性，在上线前做到心里有底。
- 单元测试可以自动化，通过编写测试用例，可以做到一次编写，多次运行。
- 驱动开发，代码被测试的前提是代码本身是可测试的，要保证代码的可测试性，就需要在开发中注意API的设计， 注意代码职责的单一性。

如何写单元测试用例？
- 测试代码时，只考虑测试，不考虑内部实现
- 数据尽量模拟实现，越靠近实现越好
- 充分考虑数据的边界条件
- 对重点、复杂、核心代码重点测试

1、Node Assert
>- JavaScript的断言规范最早来自于CommonJS的单元测试的规范, Node assert模块实现了规范中的断言部分
- 断言(assertion)：判断源码的实际执行结果与预期结果是否一致，如果不一致就抛出一个错误。
```js {.line-numbers}
 var assert = require('assert');
 assert.equal(Math.max(1,100),100);
 // 一旦 assert.equal() 不满足期望，会抛出AssertionError异常，整个程序都会停止执行
 // 没有对输出结果做出任何断言的代码，都不是测试代码
```
- 断言规范中，定义了一下几种检测方法 
>- ok() : 判断结果是否为真
>- equal() : 判断实际值与期望值是否相等
>- notEqual() : 判断实际值与期望值是否不相等
>- deepEqual() : 判断实际值与期望值是否深度相等
>- notDeepEqual() : 判断实际值与期望值是否不深度相等
>- strictEqual() : 判断实际值与期望值是否严格深度相等
>- notStrictEqual() : 判断实际值与期望值是否不严格相等
>- throws() : 判断代码块是否没有抛出异常
>- doesNotThrows() : 判断代码块是否抛出异常
>- ifError() : 判断实际值是否是为一个假值

- 断言库
>- 市面上有很多断言库都是基于assert模块进行封装和扩展,比较出名的有
1. should.js  BDD风格断言库，should.js 相对assert模块有比较丰富的API，并且其语法非常语义化
```js {.line-numbers}
var should = require('should');
(0).should.be.Number();
```
2. expect.js BDD风格断言库，语法和should相似
```js {.line-numbers}
var expect = require('expect');
expect(true).to.be.ok();
```
3. chai.js  支持BDD/TDD双模式，同时支持should/expect/assert三种风格的断言库，还有强大的插件机制
```js {.line-numbers}
var assert = requier('chai').assert
assert.notEqual(3, 4, 'these numbers are not equal')

var should = require('chai').should()
var foo = 'bar'
foo.should.be.a('string')
```
2、测试框架(mocha/Jesmine)
>- mocha 是一个功能丰富的前端测试框架。所谓"测试框架"，就是运行测试的工具。通过它，可以为JavaScript应用添加测试，从而保证代码的质量。mocha 既可以基于 Node.js 环境运行 也可以在浏览器环境运行。
  1. Mocha允许您使用任何您想要的断言库
  2. 安装：npm i mocha -g / --save-dev / -D 
  3. Mocha 测试用例主要包含下面几部分:
		 - describe 定义的测试套件(test suite)
		 - it 定义的测试用例(test case)
		 - 测试代码
		 - 断言部分
```js {.line-numbers}
// add.js 
function add(x, y) {
  return x + y;
}
module.exports = add;

// 测试脚本 add.test.js
// 测试脚本与所要测试的源码脚本同名，但是后缀名为.test.js（表示测试）或者.spec.js（表示规格）
const should = require('should');
describe("加法函数的测试",function(){
	// 用来定义测试用例 
	it('测试用例描述：1+1 = 2 ',function(){
	// 测试代码
		const n = 1 + 1; 
		// node 断言
		(3).should.equal(n,2,"message")
	})
}) 
``` 	 	 
3、测试运行工具(karma) 
- 他不是测试框架，也不是一个断言库， 他会开启一个HTTP服务，将测试文件生成一个HTML文件，在浏览器运行，调试。karma不指定测试框架，和 Mocha、jesmine 都可以结合使用
- 我们测试过程中编写的测试用例，通过它(karma)调用浏览器来运行这些测试用例，然后再汇集测试结果，生成测试报告。

- 使用步骤
>1. 安装： 
   npm install karma 
   karma-chrome-launcher
   karma-mocha -D
   npm install karma-cli -g  命令行运行   

>2. 初始化 karma init
>3. 生产配置文件
```js {.line-numbers}
# 选择测试框架，选择mocha
1. Which testing framework do you want to use ? (mocha)
# 是否引入Require.js，不需要
2. Do you want to use Require.js ? (no)
选择使用的浏览器,选择了Chrome
3. Do you want to capture any browsers automatically ? (Chrome)
# 告诉需要执行的测试用例的代码路径，支持正则
4. What is the location of your source and test files ?("test/**.js")
# 上面指定的路径中需要排除在外的文件
5. Should any of the files included by the previous patterns be excluded ? ()
# 是否观察文件的变化 
6. Do you want Karma to watch all the files and run the tests on change ? (yes)
```
>4. 运行karma karma start
 会运行测试用例，并打开chrome浏览器查看运行结果
 
4、Travis CI(Continuous Integration) 
-  持续集成 ，简称CI ：意思是，在一个项目中，任何人对代码库的任何改动，都会触发CI服务器自动对项目进行构建，自动运行测试，甚至自动部署到测试环境。这样做的好处就是，随时发现问题，随时修复。因为修复问题的成本随着时间的推移而增长，越早发现，修复成本越低
-  Travis CI 是在线托管的CI服务，用 Travis 来进行持续集成，不需要自己搭建服务器。对开源项目是免费的。
- 准备: 有 github ，也有开源项目，就可以开始 CI了 
>1. 用github账号登录travis官网，同步并激活监听github上的可测试的项目
2. 
