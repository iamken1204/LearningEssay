# Vue.js note

## Get root Vue instance's custom properties by using `$options`
```javascript
let vm = new Vue({
  myCustomProperty: 'abc123',
})
let cusPro = vm.$options.myCustomProperty
```
If you are in child components, you can use `$parent` to get parent Vue instance.
```javascript
let parentProp = this.$parent.$options.myCustomProperty
```
