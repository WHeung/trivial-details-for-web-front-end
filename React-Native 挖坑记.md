
#### 1、View元素默认且只能是flex-box
```

```
#### 2、flex-box默认flex-direction默认为column
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


#### 父元素alignItems为center后子元素在flex:1情况下宽度不能占满父容器宽度
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
    flex: 1 // 宽度不会占满父容器，而是以内容宽度缩在中间
  }
});
```
