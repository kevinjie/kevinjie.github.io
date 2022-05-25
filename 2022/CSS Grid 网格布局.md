# CSS Grid 网格布局

#CSS

Grid布局主要设置两类属性：容器属性和项目属性。

## 容器属性

### display 属性
指定一个容器采用网格布局。
```CSS
.container {
  display: grid;
}
```
### grid-template-columns、grid-template-rows
grid-template-columns设置每一列的宽度，grid-template-rows设置每一行的高度。

- 可以使用绝对单位和百分比
```CSS
.container {
  display: grid;
  grid-template-columns: 100px 100px;
  grid-template-rows: 50% 50%;
}
```
- repeat()
repeat函数 接收两个值，第一个值是重复的次数，第二个值是重复的值。
```CSS
.container {
  display: grid;
  grid-template-columns: repeat(2, 100px);
  grid-template-rows: repeat(2, 50%);
}
```

- auto-fill 关键字
如果项目的宽度固定，容器的宽度不固定，为了可以在一行中塞入尽可能多的项目，可以使用**auto-fill**关键字
```CSS
.container {
  display: grid;
  grid-template-columns: repeat(auto-fill, 100px);
}
```

- fr 关键字
为了方便表示比例关系，可以使用**fr**关键字，fr(fraction)表示片段。2fr是1fr的两倍。
```CSS
.container {
  display: grid;
  grid-template-columns: 1fr 2fr;
}
```

- minmax()
minmax 函数设置宽度在一个范围内，接收两个值，分别是最小值和最大值
```CSS
.container {
  display: grid;
  grid-template-columns: 1fr minmax(100px, 1fr);
}
```

- auto 关键字
如果让浏览器自行决定宽度，可以使用**auto**关键字
```CSS
.container {
  display: grid;
  grid-template-columns: 100px auto 100px;
}
```

- 网格线名称
可以使用方括号指定每根网格线的名称
```CSS
.container {
  display: grid;
  grid-template-columns: [c1] 100px [c2] auto [c3] 100px [c4];
  grid-template-rows: [r1] 1fr [r2] 100px [r3] 2fr [r4];
}
```

### column-gap、row-gap、gap
column-gap设置列之间的间隔，row-gap设置行之间的间隔
```CSS
.container {
  display: grid;
  grid-template-columns: 100px 100px;
  grid-template-rows: 50% 50%;
  column-gap: 10px;
  row-gap: 10px;
}
```
gap是column-gap和row-gap的合并简写形式。
```CSS
gap: <row-gap> <column-gap>;
```

### grid-template-areas
grid-template-areas用于定于区域。
```CSS
.container {
  display: grid;
  grid-template-areas: 'a b'
                       'c d';
}
```
### grid-auto-flow
grid-auto-flow用于指定容器项目的排列顺序，默认是row，即”先行后列“，设置为column，即”先列后行“。
```CSS
.container {
  display: grid;
  grid-auto-flow: row | column;
}
```
### justify-items、align-items、place-items
justify-items用于设置项目内容的水平位置，align-items用于设置项目内容的垂直位置。
```CSS
.container {
  display: grid;
  justify-items: start | end | center | stretch;
  align-items: start | end | center | stretch;
}
```
place-items是justify-items和align-items的合并简写形式。
```CSS
place-items: <align-items> <justify-items>;
```
### justify-content、align-content、place-content
justify-content用于设置整个内容区域在容器内的水平位置，align-content用于设置整个内容区域在容器内的垂直位置。
```CSS
.container {
  justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
  align-content: start | end | center | stretch | space-around | space-between | space-evenly;
}
```
place-content是justify-content和align-content的合并简写形式。
```CSS
place-content: <align-content> <justify-content>
```

## 项目属性

### grid-column-start、grid-column-end、grid-column、grid-row-start、grid-row-end、grid-row
grid-column-start和grid-column-end分别指定项目左边框和右边框所在的网格线。
grid-row-start和grid-row-end分别指定项目上边框和下边框所在的网格线。
```CSS
.container {
  display: grid;
}
.item1 {
  grid-column-start: 2;
  grid-column-end: 4;
  grid-row-start: 1;
  grid-row-end: 3;
}
```
grid-column是grid-column-start和grid-column-end的合并简写形式。
grid-row是grid-row-start和grid-row-end的合并简写形式。
```CSS
.item {
  grid-column: <start-line> / <end-line>;
  grid-row: <start-line> / <end-line>;
}
```
### grid-area
grid-area指定项目放置在哪个区域。
```CSS
.item {
  grid-area: c;
}
```
### justify-self、align-self、place-self
justify-self用于指定当前项目内容的水平位置。align-self用于指定当前项目内容的垂直位置。
```CSS
.item {
  justify-self: start | end | center | stretch;
  align-self: start | end | center | stretch;
}
```
place-self是justify-self和align-self的合并简写形式。
```CSS
place-self: <align-self> <justify-self>;
```