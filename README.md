# vue-only-number-input
a vue components that can only enter numbers

1、 引入组件
```
import onlyNumberInput from "@/components/OnlyNumberInput.vue";

components: {
    onlyNumberInput
},
```
2、 参数介绍
```
:value //输入框默认值，默认为空
:decimal //保留小数位数，默认为0，只能输入整数。
:max //输入的最大值
:min //输入的最小值
:isNeg //是否支持负数。默认false 不支持
:disabled //是否禁用。默认false 不禁用
```
3、直接使用
```
<only-number-input :decimal="8" :max="10000000000"  name="price" v-model="price"  />
//可以使用 vee-validate 插件做验证。
```
