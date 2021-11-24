---
title: Web前端开发规范(with React)
date: 2021-11-23 18:50:37
categories: Web前端
tags: [前端规范]
banner_img_height: 30
---

# Web 前端开发规范(with React)

> 不管有多少人共同参与同一项目，一定要确保每一行代码都像是同一个人编写的

## 一、概述

- 提高团队协作效率、便于后期优化维护、输出高质量的代码
- 代码即文档（编写的代码拥有一定程度的自我说明能力）
- 封装的函数/类、复杂组件、复杂的业务逻辑，需要书写注释，注释要求简练准确。不要写过多注释
- 书写 `ES6+` 的语法

## 二、环境要求

- [Node.js](https://nodejs.org/) 12 或更高版本，你可以使用 [nvm](https://github.com/creationix/nvm) 或 [nvm-windows](https://github.com/coreybutler/nvm-windows) 在一台电脑中管理多个 `Node` 版本
- 使用 [Visual Studio Code (VS Code)](https://code.visualstudio.com/) 进行代码编写
- 代码提交前要保证没有运行 bug，并且要保证代码符合规范
- 使用 Chrome 浏览器并安装 [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?utm_source=chrome-ntp-icon) 进行调试
- 使用 `Tab` 缩进，规定 Tab 大小为 `2 个空格`，保证在所有环境下获得一致展现:

```json
// vscode settings.json
{
  "editor.tabSize": 2
  // ...
}
```

## 三、编码规范

### 规范依据

- JavaScript 代码规范: [JavaScript Standard Style](https://standardjs.com/readme-zhcn.html)
- React 代码规范: [Airbnb React/JSX 风格指南](https://github.com/jiahao-c/javascript/tree/master/react)

### 具体规则

> 具体规则请阅读上述两篇文档，在此仅选取部分常见的规则进行强调与补充

#### JavaScript 常用代码规则

- 标准变量采用驼峰式命名（考虑与后台交换数据的情况，对象属性可灵活命名）
- 字符串统一使用单引号
- 不要定义未使用的变量
- 定义变量使用 `let`，定义常量使用 `const`
- 全局性、关键性的常量全大写，用下划线连接
- 变量名不应过短，要能准确完整地描述该变量所表述的事物

| 不好的变量名       | 好的变量名                   |
| ------------------ | ---------------------------- |
| inp                | input, priceInput            |
| day1, day2, param1 | today, tomorrow              |
| id                 | userId, orderId              |
| obj                | orderData, houseInfos        |
| tId                | removeMsgTimerId             |
| handler            | submitHandler, searchHandler |

- 变量名的对仗要明确，如 `up/down`、`begin/end`、`opened/closed`、`visible/invisible`、`scource/target`
- 不要使用中文拼音，如 `shijianchuo` 应改成 `timestamp` ； 如果是复数的话加 `s`，或者加上 `List`，如 `orderList`、`menuItems`； 而过去式的加上 `ed`，如 `updated/found` 等； 如果正在进行的加上 `ing`，如 `calling`
- 使用临时变量时请结合实际需要进行变量命名

_有些喜欢取 `temp` 和 `obj` 之类的变量，如果这种临时变量在两行代码内就用完了，接下来的代码就不会再用了，还是可以接受的，如交换数组的两个元素。但是有些人取了个 `temp`，接下来十几行代码都用到了这个 `temp`，这个就让人很困惑了。所以应该尽量少用 `temp` 类的变量_

```JavaScript
// not good
let temp = 10
let leftPosition = currentPosition + temp，
    topPosition = currentPosition - temp

// good
let adjustSpace = 10
let leftPosition = currentPosition + adjustSpace
let topPosition = currentPosition - adjustSpace
```

- 禁止嵌套三元表达式
- 使用箭头函数取代简单的函数

```JavaScript
// not good
let _this = this
setTimeout(function() {
  _this.foo = "bar"
}, 2000)

// good
setTimeout(() => this.foo = "bar", 2000)
```

- 禁止不必要的分号！！！

```JavaScript
window.alert('hi')   // ✓ ok
window.alert('hi');  // ✗ avoid
```

- 不要使用 `(`, `[`, or ` 等作为一行的开始，在没有分号的情况下代码压缩后会导致报错

```JavaScript
// ✓ ok
;(function () {
  window.alert('ok')
}())
// ✗ avoid
(function () {
  window.alert('ok')
}())

// ✓ ok
;[1, 2, 3].forEach(bar)
// ✗ avoid
[1, 2, 3].forEach(bar)

// ✓ ok
;`hello`.indexOf('o')
// ✗ avoid
`hello`.indexOf('o')

// 上面的正确写法是可行的，但是建议使用以下更加规范的写法

// 譬如：
;[1, 2, 3].forEach(bar)
// 建议的写法是：
let nums = [1, 2, 3]
nums.forEach(bar)
```

- 关键字后面加空格

```JavaScript
if (condition) { ... }   // ✓ ok
if(condition) { ... }    // ✗ avoid
```

- 函数声明时括号与函数名间加空格

```JavaScript
function name (arg) { ... }   // ✓ ok
function name(arg) { ... }    // ✗ avoid

run(function () { ... })      // ✓ ok
run(function() { ... })       // ✗ avoid
```

- 函数调用时标识符与括号间不留间隔

```JavaScript
console.log ('hello') // ✗ avoid
console.log('hello')  // ✓ ok
```

- 始终使用 === 替代 ==

```JavaScript
if (name === 'John')   // ✓ ok
if (name == 'John')    // ✗ avoid

if (name !== 'John')   // ✓ ok
if (name != 'John')    // ✗ avoid
```

- 文件末尾留一空行

#### React 相关规范

##### 主要使用技术栈

- UI 组件库 [Antd](https://ant-design.gitee.io/index-cn)
- 图表库 [Ant Design Charts](https://charts.ant.design/zh-CN)
- 开箱即用的中台前端/设计解决方案 [Ant Design Pro](https://pro.ant.design/index-cn)
- 高度封装的业务组件库 [ProComponents](https://procomponents.ant.design/)
- 插件化的企业级前端应用框架 [UmiJS](https://umijs.org/zh-CN)

##### React 常用代码规则

**组件**

**1. 基本规则**

- 一个文件最多只能包含一个 `class` 组件，可以包含多个 `function` 组件
- 使用 `JSX` 语法
- 使用 `class`、`function` 或 `Hooks` 声明组件，不使用 `React.createElement`

**2. 组件名**

- 组件名称和定义该组件的文件名称尽量保持一致，名称尽量简短

```JavaScript
// Good
import MyComponent from './MyComponent'

// Bad
import MyComponent from './MyComponent/index'
```

- 应在 `class`、`function`(箭头函数就是 `const` 关键字) 关键字或 声明后面直接声明组件名称,不要使用 `displayName` 来命名 `React` 模块

```JavaScript
// Good
export default class MyComponent extends React.Component {}

const MyField = (props) => {
  return <></>
}

// bad
export default React.createClass({
  displayName: 'MyComponent',
})
```

- 组件名称应全局唯一

_很多业务都会有相同的文件命名，此时应在声明组件名称时保持全局唯一。一般是将业务链路名称全拼至组件声明_

```JavaScript
// Account/User/List.jsx

// Good
export default class AccountUserList extends React.Component {}

// Bad
export default class List extends React.Component {}
```

- 高阶组件名

```JavaScript
// Bad
export default function withFoo(WrappedComponent) {
  return function WithFoo(props) {
    return <WrappedComponent {...props} foo />
  }
}

// Good
export default function withFoo(WrappedComponent) {
  function WithFoo(props) {
    return <WrappedComponent {...props} foo />
  }

  const wrappedComponentName =
    WrappedComponent.displayName || WrappedComponent.name || 'Component'

  WithFoo.displayName = `withFoo(${wrappedComponentName})`
  return WithFoo
}
```

**1. 组件文件名**

- 组件文件后缀为 `jsx`、`tsx`
- 组件文件名为 `PascalCase` 大驼峰格式

```bash
components/
|- MyComponents.jsx
```

- 组件文件夹名称和默认导出一个组件可以被拆分成多个组件编写的应建立目录，目录使用 PascalCase。建立 index.jsx 导出对象

```bash
components/
|- MyComponent/
|----index.jsx
|----MyComponentList.jsx
|----MyComponentListItem.jsx
```

**4. Hooks**

- `Function` + `Hooks` 形式的组件优先，尽量少写 `Class` 组件

```jsx
// Good
import React, { useState, useEffect } from 'react'
import { Modal, Form, Checkbox } from 'antd'

const AutoModal = props => {
  const { visible, formItemLayout, customerFlag, csFlag } = props
  const [confirmLoading, setConfirmLoading] = useState(false)
  const [form] = Form.useForm()
  const [csFlagState, setCsFlagState] = useState(csFlag)
  const [customerFlagState, setCustomerFlagState] = useState(customerFlag)
  const handleFinish = async values => {
    try {
      setConfirmLoading(true)
      await handleOk(values)
    } catch (e) {
      console.error(e)
    } finally {
      setConfirmLoading(false)
    }
  }
  const handleOk = () => {
    form.submit()
  }
  const handleCancel = () => {}
  const handleCSFlagChange = e => {
    setCsFlagState(e.target.checked)
  }
  const handleCustomerFlagChange = e => {
    setCustomerFlagState(e.target.checked)
  }
  const checkFlag = () => {
    if (csFlagState || customerFlagState) {
      return Promise.resolve()
    }
    message.warning('服务客服或服务客户至少选一项')
    return Promise.reject(new Error('服务客服或服务客户至少选一项'))
  }

  useEffect(() => {
    // 使用visible防止出现useForm报错
    if (visible) {
      form.setFieldsValue({
        newTskId: modifyObj.tskId,
        creIdList: modifyObj.creIdList,
        custIdList: modifyObj.custIdList,
      })
    }
  }, [modifyObj, visible, form])

  useEffect(() => {
    if (visible) {
      form.setFieldsValue({
        csFlag,
      })
      setCsFlagState(csFlag)
    }
  }, [csFlag, visible, form])

  useEffect(() => {
    if (visible) {
      form.setFieldsValue({
        customeFlag: customerFlag,
      })
      setCustomerFlagState(customerFlag)
    }
  }, [customerFlag, visible, form])

  return (
    <Modal
      forceRender
      title={title}
      visible={visible}
      onOk={handleOk}
      confirmLoading={confirmLoading}
      onCancel={handleCancel}
      destroyOnClose
    >
      <Form
        form={form}
        preserve={false}
        onFinish={handleFinish}
        layout="horizontal"
        {...formItemLayout}
      >
        <Form.Item
          {...formItemLayout}
          style={{ marginBottom: 0 }}
          label={
            <Form.Item
              noStyle
              name="csFlag"
              rules={[{ validator: checkFlag }]}
              validateTrigger="onSubmit"
              initialValue={csFlagState}
              valuePropName="checked"
            >
              <Checkbox onChange={handleCSFlagChange}>{csLabel}</Checkbox>
            </Form.Item>
          }
        ></Form.Item>
        <Form.Item
          {...formItemLayout}
          style={{ marginBottom: 0 }}
          label={
            <Form.Item
              noStyle
              name="customeFlag"
              rules={[{ validator: checkFlag }]}
              validateTrigger="onSubmit"
              initialValue={customerFlagState}
              valuePropName="checked"
            >
              <Checkbox onChange={handleCustomerFlagChange}>
                {customerLabel}
              </Checkbox>
            </Form.Item>
          }
        ></Form.Item>
      </Form>
    </Modal>
  )
}

export default AutoModal
```

**5. 组件中的命名规则**

- 属性名称： 使用小驼峰命名
- style 样式： 使用小驼峰命名的样式属性

**6. 组件样式**

- 使用 `CSS Modules` 编写局部样式组件，因为其对象是作为对象在 jsx 中使用，样式应使用小驼峰命名

```JavaScript
.myWrapper {
  &-Text {
  }
}

import styles from 'style.less'

export default class MyComponent extends React.Component {
  render() {
    return (
      <div className={styles.myWrapper}>
        <p className={styles.myWrapperText}></p>
      </div>
    )
  }
}
```
