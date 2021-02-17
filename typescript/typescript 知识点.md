#### Typescript 知识点

```javascript
class LeftMenuProps extends Vue {
  @Prop({ type: Array, default: [] })
  list!: CategoryModel[];
}
// ! 代表null or undefined
```

#### typescript for event element

``` javascript
const target = this.$refs.input as HTMLInputElement;
target.value // can read it
```

