# useEffect和useLayoutEffect的区别

#react

- useLayoutEffect 与 componentDidMount 和 componentDidUpdate 的触发时机一致，即在DOM修改之后页面渲染之前
- useEffect比useLayoutEffect触发时机要晚，在页面渲染之后
- useLayoutEffect 切忌执行一些同步耗时操作，会阻塞浏览器渲染
