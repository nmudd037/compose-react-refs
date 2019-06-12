# Compose react refs

A simple utility for composing two or more
[react refs](https://reactjs.org/docs/refs-and-the-dom.html) (ref objects and
callbacks are both supported and can be mixed) into a single callback ref.

This utility does not use
[react hooks](https://reactjs.org/docs/hooks-intro.html), therefore it can be
used in class components (and even outside of react world) safely.

## Installation

`compose-react-refs` is available as npm package, you can use `npm` to install
it:

```
npm install --save @seznam/compose-react-refs
```

## Usage

The following example shows usage in a functional component that composes an
external ref with its own ref it uses to focus the renderer `<input>` element:

```typescript jsx
import * as React from 'react'
import composeRefs from '@seznam/compose-react-refs'

export default React.forwardRef((props, externalRef) => {
  const myRef = React.useRef(null)
  
  React.useEffect(() => {
    myRef.current.focus()
  })

  return <input {...props} ref={composeRefs(myRef, externalRef)}/>
})
```

The refs will be updated in the order in which they were provided to the
`composeRefs` function.
