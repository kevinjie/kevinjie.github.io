### 前端测试是什么

#test

> 为检测特定的目标是否符合标准而采用专用的工具或者方法进行验证，并最终得出特定的结果。

   对于前端开发过程来说，这里的特定目标就是指我们写的代码，而工具就是我们需要用到的测试框架(库)、测试用例等。检测处的结果就是展示测试是否通过或者给出测试报告，这样才能方便问题的排查和后期的修正。
### 测试的意义
1.	验证代码的正确性
2.	利用测试自动化，提高效率
3.	驱动开发，指导设计
4.	保证重构的安全性
### 单元测试的原则
1.	测试代码时，只考虑测试，不考虑内部实现
2.	数据尽量模拟现实，越靠近现实越好
3.	充分考虑数据的边界条件
4.	对重点、复杂、核心代码，重点测试
5.	利用AOP(beforeEach、afterEach),减少测试代码数量，避免无用功能
6.	测试、功能开发相结合，有利于设计和代码重构
### 测试方法论
+ TDD（Test-driven development）
基本思路是通过测试来推动整个开发的进行
    1.	需求分析，思考实现，先写测试再写代码
    2.	实现代码让测试通过
    3.	优化代码让测试通过
    4.	一般结合单元测试
    5.	测试重点在代码
    6.	测试速度快
+ BDD(Behavior-driven development)
通过分析用户的行为，测试产品的运行结果是否符合预期
    1.	需求分析，先写代码实现功能
    2.	写测试用例验证用户行为
    3.	一般结合集成测试
    4.	测试重点在UI（DOM）
    5.	测试速度慢
### 测试工具
+ 测试框架
测试框架的作用是提供一些方便的语法来描述测试用例，以及对用例进行分组。
常见的测试工具有常见的测试框架有 [Jasmine](https://link.juejin.im/?target=https%3A%2F%2Fjasmine.github.io%2F), [Mocha](https://link.juejin.im/?target=https%3A%2F%2Fmochajs.org%2F) 以及 [Jest](https://link.juejin.im/?target=http%3A%2F%2Ffacebook.github.io%2Fjest%2Fzh-Hans%2F) 
+ 断言库
断言库主要提供语义化方法，用于对参与测试的值做各种各样的判断。
常见的断言库有 [Should.js](https://link.juejin.im/?target=https%3A%2F%2Fshouldjs.github.io%2F), [Chai.js](https://link.juejin.im/?target=http%3A%2F%2Fchaijs.com%2F) 等。
+ 测试覆盖率工具
用于统计测试用例对代码的测试情况，生成相应的报表，比如 [istanbul](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fgotwarlost%2Fistanbul) 。
### Jest
+ 为什么使用Jest
Jest 是 Facebook 出品的一个测试框架，相对其他测试框架，其一大特点就是就是内置了常用的测试工具，比如自带断言、测试覆盖率工具，实现了开箱即用。
而作为一个面向前端的测试框架， Jest 可以利用其特有的快照测试功能，通过比对 UI 代码生成的快照文件，实现对 React 等常见框架的自动测试。
此外， Jest 的测试用例是并行执行的，而且只执行发生改变的文件所对应的测试，提升了测试速度。
Jest对常见框架的支持较好，React的脚手架create-react-app内部集成Jest，新建项目之后配合enzyme测试库即可开始编写测试用例；Vue-cli 3.0的脚手架可以在安装时选择Jest，配合Vue-test-utils测试库即可开始编写测试用例。
+ Jest的功能
    + 钩子函数
        * beforeAll,beforeEach,afterAll,afterEach可以处理一些公共的逻辑
    + 修饰符
        * .only 只测试当前用例或集
        * .skip跳过当前用例或集
        * .each使用测试数据重复测试当前用例或集
        * .only.each使用测试数据只重复测试当前用例或集
    + 匹配器
        * 判断测试的结果是否符合预期
    + Mock 函数
        * Mock函数提供的一系列方法用来mock返回
    + Jest方法
        * 用来帮助创建mock，控制jest的行为
    + 监测模式
        * a模式，运行所有测试文件，等同于jest —watchAll
        * f模式，只运行失败的测试方法
        * o模式，只运行修改过的（相比较于仓库中的代码）测试文件，等同于 jest —watch，必须是用git初始化过的项目
        * p模式，根据文件名称正则表达式确定哪些文件需要运行测试，需要 jest —watchAll
        * t模式，根据测试用例名称正则表达式确定哪些文件需要运行测试
        * q模式，退出测试
+ Jest使用方法
    + 初始化jest配置
      * 运行``npm jest —init``命令
      在根目录生成一个jest.config.js文件，文件中包含默认配置和注释，可以根据需求修改
    + 异步测试方法
      * mock axios
      ```
      // fetchData.js
      import axios from 'axios'

      export const fetchData = () => {
        return axios.get('/api').then(res => res.data)
      }

      export const fetchDataCallback = (fn) => {
        return axios.get('./api').then(res => {
            fn(res.data)
        })
      }

      // fetchData.test.js
      import { fetchData, fetchDataCallback } from './fetchData'
      import axios from 'axios'
      jest.mock('axios')

      describe('test fetchData', async () => {
        it('test fetchData', () => {
          axios.get.mockResolvedValue({ data: 'hello' })
          await fetchData().then(data => {
            expect(data).toBe('hello')
          })
        })

        it('test fetchDataCallback', (done) => {
          axios.get.mockResolvedValue({ data: 'hello' })
          fetchDataCallback(data => {
            expect(data).toBe('hello')
            done()
          })
        })
      })

      ```
    + 钩子函数的使用
      ```
      // 使用一组数据循环调用测试用例
      it.each([[1, 2, 3], [1, 1, 2]])('add to be expected', (a, b, expected) => {
        expect(a + b).toBe(expected)
      })

      // 跳过该测试用例
      it.skip('test add', () => {
        expect(1 + 2).toBe(3)
      })

      // 只测试当前用例
      it('test only', () => {
        expect(1 + 2).toBe(3)
      })
      ```
    + mock
      * mock callback
      ```
      // callback.js
      export const runCallback = function (callback) {
        callback()
      }

      // callback.test.js
      import { runCallback } from './callback'

      describe('test callback mock', () => {
        it('test callback', () => {
          const func = jest.fn()
          // const func = jest.fn(() => {
          //    return 'abc'
          // })
          func.mockReturnValue('abc')
          // func.mockImplementation(() => {
          //    return 'abc'
          // })
          runCallback(func)
          runCallback(func)
          expect(func).toBeCalledTimers(2)
          expect(func.mock.results[0].value).toEqual('abc')
        })
      })
      ```
      mock timer
      ```
      // timer.js
      export default (cb) => {
        setTimeout(() => {
          cb()
          setTimeout(() => {
            cb()
          }, 3000)
        }, 3000)
      }

      // timer.test.js
      import timer from './timer'
      jest.useFakeTimers()
      describe('test', () => {
        it('test timer', () => {
          const func = jest.fn()
          timer(func)
          // jest.runAllTimers()
          // jest.runOnlyPendingTimers()
          jest.runTimersToTime(6000)
          expect(func).toHaveBeenCalledTimes(1)
        })
      })
      ```
    + snapshot快照测试
      ```
      // snapshot.test.js
      import { shallowMount } from '@vue/test-utils'
      import HelloWorld from '@/components/HelloWorld.vue'

      describe('test snapshot', () => {
        it('test snapshot', () => {
          const wrapper = shallowMount(HelloWorld)
          expect(wrapper).toMatchSnapshot()
        })
      })
      ```
    + ES6类的测试
      ```
      // util.js
      class Util {
        init () {
          // ...
        }

        a () {
          // ...
        }

        b () {
          // ...
        }
      }

      export default Util

      // demoFunction.js
      import Util from './util'

      const demoFunction = (a, b) => {
        const util = new Util()
        util.a()
        util.b()
      }
      export default demoFunction

      // demoFunction.spec.js
      import demoFunction from './demoFunction'
      import Util from './util'
      jest.mock('./util')
      // jest.mock('./util', () => {
      //   const Util = jest.fn()
      //   Util.prototype.a = jest.fn()
      //   Util.prototype.b = jest.fn()
      //   return Util
      // })

      describe('test class', () => {
        it('test demoFunction', () => {
          demoFunction()
          console.log(Util.mock)
          expect(Util).toHaveBeenCalled()
          expect(Util.mock.instances[0].a).toHaveBeenCalled()
          expect(Util.mock.instances[0].b).toHaveBeenCalled()
        })
      })
      ```
    + DOM节点操作测试
        * jest在node环境模拟了一套dom的api，jsDom，可以直接操作dom
### Vue中的Jest的使用
+ 安装
以Vue-cli 3.0为例，展示安装配置方法
    + 首先在terminal中新建一个项目
    ``vue create jest-vue``
    + 选择 Manually select features
    + 测试方案选择Jest，其他根据个人情况选择
    至此Vue下的Jest测试已经安装配置好了，就是这么简单
    Jest的所有配置文件在jest.config.js中，具体配置含义可以参考官方文档。所有以.spec.js、.test.js结尾或者在__tests__中的所有文件都会被认为是测试文件。
+ vue-test-utils测试库

  [Vue Test Utils](https://vue-test-utils.vuejs.org/zh/)

  ```
  // example.spec.js
  import { mount } from '@vue/test-utils'
  import HelloWorld from '@/components/HelloWorld.vue'

  describe('has a', () => {
    it('has a', () => {
    const wrapper = mount(HelloWorld)
    expect(wrapper.contains('a')).toBe(true)
    })
  })
  ```

### React中的Jest的使用
+ 安装
以Create-react-app脚手架工具，展示安装配置方法
    + 首先在terminal中新建一个项目
    ``create-react-app jest-react``
    + 弹出隐藏的配置文件
    ``npm run eject``
    + 安装enzyme相关依赖
    ```
    yarn add --dev enzyme jest-environment-enzyme jest-enzyme enzyme-adapter-react-16
    ```
    + 调整package.json
    ```
    ”jest": {
      "setupFilesAfterEnv": ["jest-enzyme"],
      "testEnvironment": "enzyme"
     }
     ```
    Jest的配置在package.json中，具体配置含义可以参考官方文档。所有以.spec.js、.test.js结尾或者在_tests_中的所有文件都会被认为是测试文件。
+ enzyme测试库

  [enzyme](https://github.com/airbnb/enzyme)
  ```
  import React from 'react';
  import { shallow } from 'enzyme'
  import App from './App';

  it('renders without crashing', () => {
    const wrapper = shallow(<App />)
    expect(wrapper.find('.App-header').length).toBe(1)
  });
  ```
### ES6和Node项目使用jest
+ 使用``npm init``命令，把项目变成一个npm包
+ 安装jest ``yarn add --dev jest``
+ 修改package.json文件，在script中，添加test: jest命令
+ 对需要测试的abc.js文件改造，把需要测试的方法添加
  ```
  try {
    module.exports = {
      // functions
    }
  } catch(e) {}
  ```
+ 在要做测试的js文件同级目录新建一个同名以.test.js结尾的文件
+ 在.test.js文件中引入需要测试的方法写测试用例
  ```
  const func = require('./abc')
  const {/*funcs*/} = func
  ```
+ 执行 ``npm run test``命令运行测试用例

### 持续集成测试
为了满足持续集成测试的需求，我们需要借助git hook来帮助我们自动触发测试。
Husky可以帮助我们设置本地的Git hook，利用pre-commit钩子在每次代码commit之前，执行必要的自动化测试，以达到提高代码质量的要求。
在terminal中运行以下命令安装husky
``yarn add —dev husky``
在package.json中配置
```
”husky": {
  "hooks": {
    ”pre-commit": "npm run test" // pre-commit，提交前的钩子
  }
}
```
如果需要结合Jenkins和Gerrit来部署测试方案，可以参考以下方案
[Jenkins + Gerrit + Git自动部署测试](https://blog.csdn.net/mr_raptor/article/details/76223233)
### 参考资料
* [jest](https://jestjs.io/)
* [enzyme](https://github.com/airbnb/enzyme)
* [husky](https://github.com/typicode/husky)
* [The Difference Between TDD and BDD](https://joshldavis.com/2013/05/27/difference-between-tdd-and-bdd/)
* [Vue Test Utils](https://vue-test-utils.vuejs.org/zh/)
* [Jenkins + Gerrit + Git自动部署测试](https://blog.csdn.net/mr_raptor/article/details/76223233)
