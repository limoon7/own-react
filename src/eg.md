```js
// 通过id获取一个元素
const domRoot = document.getElementById("root");
// 创建一个给定标签名称的新元素
const domInput = document.createElement("input");
// 设置元素属性
domInput["type"] = "text";
domInput["value"] = "Hi world";
domInput["className"] = "my-class";
// 监听事件
domInput.addEventListener("change", e => alert(e.target.value));
// 创建一个文本节点
const domText = document.createTextNode("");
// 设置文本节点内容
domText["nodeValue"] = "Foo";
// 增加一个元素
domRoot.appendChild(domInput);
// 增加一个文本节点
domRoot.appendChild(domText);
```

```js
const element = {
  type: "div",
  props: {
    id: "container",
    children: [
      { type: "input", props: { value: "foo", type: "text" } },
      { type: "a", props: { href: "/bar" } },
      { type: "span", props: {} }
    ]
  }
};

<div id="container">
  <input value="foo" type="text">
  <a href="/bar"></a>
  <span></span>
</div>


```

```js
function render(element, container) {
  const dom =
    element.type == "TEXT_ELEMENT"
      ? document.createTextNode("")
      : document.createElement(element.type)
​
  const isProperty = key => key !== "children"
  Object.keys(element.props)
    .filter(isProperty)
    .forEach(name => {
      dom[name] = element.props[name]
    })
​
  element.props.children.forEach(child =>
    render(child, dom)
  )
​
  container.appendChild(dom)
}
```

```js
const element = (
  <div id="container">
    <input value="foo" type="text">
    <a href="/bar"></a>
    <span></span>
  </div>
);

```

```js
const element = React.createElement(
  "div",
  { id: "container" },
  React.createElement("input", { value: "foo", type: "text" }),
  React.createElement(
    "a",
    { href: "/bar" },
    "bar"
  ),
  React.createElement(
    "span",
  )
);
```
