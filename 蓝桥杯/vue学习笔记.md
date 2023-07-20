## vue学习笔记



### props

参数说明:

+ `type`：指定prop的数据类型。它可以是以下原生构造函数之一：String、Number、Boolean、Array、Object、Date、Function、Symbol。你还可以用一个数组列出多个有效的类型，如 `[String, Number]`。

+ `default`：为prop提供一个默认值。如果父组件未提供prop值，那么子组件会使用此默认值。对于对象和数组类型的prop，应使用函数返回默认值，以避免它们在组件实例之间共享。
+ `required`：指定prop是否必须。设置为`true`时，如果父组件未提供此prop，Vue将发出警告。
+ `validator`：为prop提供一个自定义验证函数。函数应返回一个布尔值。如果返回`false`，Vue将发出警告。

示例:

```js
export default {
  props: {
    colorClass: {
      type: String,
      default: 'default-color-class',
      required: true,
      validator: function (value) {
      // 允许的状态值
      	  const validStatuses = ['danger', 'primary', 'waiting'];
      	  return validStatuses.includes(value);
      },
    },
    value: {
      type: Number,
      default: 0,
    },
    items: {
      type: Array,
      default: () => [],
    },
  },
};
```

注意: 组件传递props时直接赋值传递的参数默认类型为`String`,传递JS表达时要使用`v-bind`语法
