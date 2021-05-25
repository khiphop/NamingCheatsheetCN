## 英语

使用英语命名变量和方法名

```js
/* 反例 */
# 西班牙语
const primerNombre = 'Gustavo'
const amigos = ['Kate', 'John']

/* 规范 */
const firstName = 'Gustavo'
const friends = ['Kate', 'John']
```

> 不管你喜不喜欢, 英语是编程中都是处统治地位: 所有编程语言的语法都是用英语编写, 同样的还有不计其数的文献和教学材料. 你通过英语写代码会增加它的流通性和可读性



## 命名规范
选择 **一个** 命名规范并贯彻它. 不管是 `camelCase(驼峰命名法)`, `PascalCase(帕斯卡命名法)`, `snake_case(下划线命名法)`还是其他的方法, 都要始终保持一致. 就命名规范来说很多编程语言有他们的传统; 看看这份文档是否适合你, 也可以在Github上参考好的项目



```js
/* 反例 */
const page_count = 5
const shouldUpdate = true

/* 规范1 */
const pageCount = 5
const shouldUpdate = true

/* 规范2 */
const page_count = 5
const should_update = true
```

## S-I-D

命名必需保持 _简短_, _直观_, _形象_:
- **简短**. 一个命名决不能太长, 不利于写和记;
- **直观**. 一个命名必需读起来自然, 尽可能贴近常用的说法;
- **形象**. 一个命名必需高效的反映它是做什么用的.

```js
/* 反例 */
const a = 5 // "a" 可以表示任何东西
const isPaginatable = a > 10 // "Paginatable" 很拗口
const shouldPaginatize = a > 10

/* 规范 */
const postCount = 5
const hasPagination = postCount > 10
const shouldPaginate = postCount > 10 // 二者选其一
```

## 避免缩写

**不要** 使用缩写 —— 缩写只会降低代码的可读性. 想找一个简短, 形象的名字确实很难, 但这不是使用缩写的理由.


```js
/* 反例 */
const onItmClk = () => {}

/* 规范 */
const onItemClick = () => {}
```

## 避免与语境重复

命名不应该重复已经定义过的语境. 如果不能提升可读性, 就应该把语境从命名中移出.

```js
class MenuItem {
  /* 方法名跟语境重复 (MenuItem) */
  handleMenuItemClick = (event) => { ... }

  /* `MenuItem.handleClick()` 读起来好多了*/
  handleClick = (event) => { ... }
}
```

## 表达期望的结果

一个命名应当表达出期望的结果.

```jsx
/* 反例 */
const isEnabled = itemCount > 3
return <Button disabled={!isEnabled} />

/* 规范 */
const isDisabled = itemCount <= 3
return <Button disabled={isDisabled} />
```

---

# 命名方法

## A/HC/LC 模式

这是个有用的命名方法的模式:


```
前缀? + 行为 (A) + 高语境 (HC) + 低语境? (LC)
```

```
prefix? + action (A) + high context (HC) + low context? (LC)
```

通过以下表格看看这个模式是怎么应用的.

| 命名                   | 前缀   | 行为 (A) | 高语境 (HC) | 低语境 (LC) |
| ---------------------- | -------- | ---------- | ----------------- | ---------------- |
| `getUser`              |          | `get`      | `User`            |                  |
| `getUserMessages`      |          | `get`      | `User`            | `Messages`       |
| `handleClickOutside`   |          | `handle`   | `Click`           | `Outside`        |
| `shouldDisplayMessage` | `should` | `Display`  | `Message`         |                  |

> **注解** 语境的顺序影响变量的含义. 例如, `shouldUpdateComponent` 表示 _你_ 将要更新一个组件, 而 `shouldComponentUpdate` 表示 _组件_ 会自我更新, 而你只是控制他是否该更新.

> 换句话说, **高语境** 强调了变量的含义


---

## 行为

你方法名的动态部分. 负责最重要的部分——阐释你的方法是做什么的.

### `get`

快速获取数据.

```js
function getFruitCount() {
  return this.fruits.length
}
```

> 另请参考 [compose](#compose).

### `set`

声明将变量从 `A` 设为 `B`.

```js
let fruits = 0

function setFruits(nextFruits) {
  fruits = nextFruits
}

setFruits(5)
console.log(fruits) // 5
```

### `reset`

将一个变量重置为它的初始值或状态.

```js
const initialFruits = 5
let fruits = initialFruits
setFruits(10)
console.log(fruits) // 10

function resetFruits() {
  fruits = initialFruits
}

resetFruits()
console.log(fruits) // 5
```

### `fetch`

请求获取一些数据, 消耗时间不确定(也即 异步请求).


```js
function fetchPosts(postCount) {
  return fetch('https://api.dev/posts', {...})
}
```

### `remove`

_从_ 某处移除一些东西.

例如, 如果你在搜索页上有一个选中的筛选条件集合, 从集合中移除一项就是 `removeFilter`, **而不是** `deleteFilter` (你平时英语口语也应该这么说):


```js
function removeFilter(filterName, filters) {
  return filters.filter((name) => name !== filterName)
}

const selectedFilters = ['price', 'availability', 'size']
removeFilter('price', selectedFilters)
```

> 另请参考 [delete](#delete).

### `delete`

从存在的领域完全擦除一些信息.

想象一下你是一个文章编辑者, 你想丢弃一些糟糕的帖子. 当你点击了一个闪亮的"Delete post"按钮, CMS应该执行 `deletePost` 功能, **而不是**  `removePost`功能.


```js
function deletePost(id) {
  return database.find({ id }).delete()
}
```

> 另请参考 [remove](#remove).

### `compose`

从存在的个体上创造新数据. 主要适用于字符串, 结构体, 或者方法.

```js
function composePageUrl(pageName, pageId) {
  return (pageName.toLowerCase() + '-' + pageId)
}
```

> 另请参考 [get](#get).

### `handle`

处理一个行为. 经常用来命名回调方法.

```js
function handleLinkClick() {
  console.log('Clicked a link!')
}

link.addEventListener('click', handleLinkClick)
```

---

## 语境

方法所操作的领域.

一个方法通常是操作某些事物的动作. 需要申明它可操作的空间, 最起码说明期望的数据类型.

```js
/* 一个操作原数据的简单方法 */
function filter(list, predicate) {
  return list.filter(predicate)
}


/* 方法操作完全基于请求参数 */
function getRecentPosts(posts) {
  return filter(posts, (post) => post.date === Date.now())
}
```

> 一些特定语言的情况会允许省略语境. 比如, 在JavaScript中, `filter`一般是操作数组(Array)的, 明确地使用`filterArray`反而是多余的.



---

## 前缀

前缀让命名更易于理解. 较少用在方法名.

### `is`

描述当前语境下的一个特征或状态(通常是`布尔值`).


```js
const color = 'blue'
const isBlue = color === 'blue' // characteristic
const isPresent = true // state

if (isBlue && isPresent) {
  console.log('Blue is present!')
}
```

### `has`

描述当前语境是否拥有一个特定值或状态(通常是`布尔值`).

```js
/* 反例 */
const isProductsExist = productsCount > 0
const areProductsPresent = productsCount > 0

/* 规范 */
const hasProducts = productsCount > 0
```

### `should`

反映一个动作的条件状态(通常是 `布尔值`)

```js
function shouldUpdateUrl(url, expectedUrl) {
  return url !== expectedUrl
}
```

### `min`/`max`

表示一个最大或最小值. 用在描述临界的情况

```js
/**
 * 根据给出的最大最小范围取出随机数量的posts.
 */
function renderPosts(posts, minPosts, maxPosts) {
  return posts.slice(0, randomBetween(minPosts, maxPosts))
}
```

### `prev`/`next`


指明在当前环境下一个变量的前一个或下一个状态. 用在表达状态转换的时候.

```jsx
function fetchPosts() {
  const prevPosts = this.state.posts

  const fetchedPosts = fetch('...')
  const nextPosts = concat(prevPosts, fetchedPosts)

  this.setState({ posts: nextPosts })
}
```

## 单数和复数

就像前缀, 变量可以根据处理了一个或多个值来命名成单数或复数.


```js
/* 反例 */
const friends = 'Bob'
const friend = ['Bob', 'Tony', 'Tanya']

/* 规范 */
const friend = 'Bob'
const friends = ['Bob', 'Tony', 'Tanya']
```
