
#### 1、The View element can only be flex-box by default
```

```
#### 2、flex-box default flex-direction defaults to column
flex-box默认flex-direction默认为column
```
<View style={styles.main}>
</View>
StyleSheet.create({
  main: {
    flex: 1,
    flexDirection: 'column' // 默认
  }
});
```


#### After the parent element alignItems is center, the width of the child element cannot occupy the width of the parent container in the case of flex: 1
父元素alignItems为center后子元素在flex:1情况下宽度不能占满父容器宽度
```
<View style={styles.main}>
    <View style={styles.child}>
    </View>
</View>
StyleSheet.create({
  main: {
    flex: 1,
    alignItems: 'center',
  },
  select: {
    flex: 1 // The width will not fill the parent container, but shrink in the middle with the content width (宽度不会占满父容器，而是以内容宽度缩在中间)
  }
});
```
