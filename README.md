## ompjs

Object data mapping tool library.
[中文文档](./zh.md)
## Install

```bash
yarn add ompjs
```

## Usage

```js
import { mapping as mappingFn, usePipeline} from 'ompjs'

const source = {
  a: '1',
  b: 4,
  c: '2',
  d: '2022/01/18'
}

const mapping = {
  e: 'a|number',
  f: 'b|string',
  g: 'c|boolean',
  h: 'd|date'
}

const result = mappingFn(obj, mapping)

// {
//   e: 1,
//   f: '4',
//   g: true,
//   h: '2022-01-17T16:00:00.000Z'
// }
```

### Custom Pipeline

```js
import { mapping as mappingFn, usePipeline} from 'ompjs'

usePipeline({
  camel: (v:string)=> {
    return v.replace(/\_(\w)/g, (all, letter) => {
      return letter.toUpperCase()
    })
  }
})
const obj = {
  a: 'abc_def'
}
const mapping = {
  e: 'a|camel',
}
const result = mappingFn(obj, mapping)

// {
//  e: 'abcDef'
// }
```

### Multiple Pipeline

```js
import { mapping as mappingFn, usePipeline} from 'ompjs'

usePipeline({
  month: (v:Date)=> {
    return v.getMonth() + 1
  }
})
const obj = {
  a: '2022/01/18'
}
const mapping = {
  month: 'a|date|month',
}
const result = mappingFn(obj, mapping)
// {
//  month: 1
// }
```