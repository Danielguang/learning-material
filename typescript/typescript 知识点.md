#### Typescript 知识点

```javascript
class LeftMenuProps extends Vue {
  @Prop({ type: Array, default: [] })
  list!: CategoryModel[];
}
// ! 代表null or undefined
```

