# React项目

项目描述：后台管理系统





UI antd 框架

引入antd 框架

```
npm i antd
```

 使用antd 框架

```jsx
import {Button} from 'antd'; //引入antd
import 'antd/dist/antd.css';//引入组件css样式
export default class Login extends React.Component{
    render(){
      return(
           <Button>我antd的按钮</Button>
      )
      
    }
};
```

通过设置 Button 的属性来产生不同的按钮样式，推荐顺序为：`type` -> `shape` -> `size` -> `loading` -> `disabled`。

按钮的属性说明如下：

| 属性     | 说明                                                         | 类型                         | 默认值    | 版本  |
| :------- | :----------------------------------------------------------- | :--------------------------- | :-------- | :---- |
| disabled | 按钮失效状态                                                 | boolean                      | `false`   | 3.5.1 |
| ghost    | 幽灵属性，使按钮背景透明，版本 2.7 中增加                    | boolean                      | false     |       |
| href     | 点击跳转的地址，指定此属性 button 的行为和 a 链接一致        | string                       | -         |       |
| htmlType | 设置 `button` 原生的 `type` 值，可选值请参考 [HTML 标准](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button#attr-type) | string                       | `button`  |       |
| icon     | 设置按钮的图标类型                                           | string                       | -         |       |
| loading  | 设置按钮载入状态                                             | boolean \| { delay: number } | `false`   |       |
| shape    | 设置按钮形状，可选值为 `circle`、 `round` 或者不设           | string                       | -         |       |
| size     | 设置按钮大小，可选值为 `small` `large` 或者不设              | string                       | `default` |       |
| target   | 相当于 a 链接的 target 属性，href 存在时生效                 | string                       | -         |       |
| type     | 设置按钮类型，可选值为 `primary` `dashed` `danger` `link`(3.17 中增加) 或者不设 | string                       | -         |       |
| onClick  | 点击按钮时的回调                                             | (event) => void              | -         |       |
| block    | 将按钮宽度调整为其父宽度的选项                               | boolean                      | `false`   | 3.8.0 |

  [进行官网详情了解](https://ant.design/components/button-cn/ )

高级配置

```
npm i react-app-rewired customize-cra
```

 [配置步骤](https://ant.design/docs/react/introduce-cn)

