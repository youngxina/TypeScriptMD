### TypeScript + Vue3

由于在公司中开发的技术栈为Vue3+TypeScript，所以就总结一些Vue3+TypeScript开发的相关内容

以下内容全部采取Composition API演示

首先我们要确保组件的script部分已经将语言设置为TypeScript， 并且引入defineComponent

```vue
<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
	...
})
</script>
```

#### 常用的

```
1. ref<T>
2. reactive<T>
```

