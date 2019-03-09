# Typed css-in-js

CSS-in-JS solution with good typing support and zero-runtime.

## Modifiers

```javascript
// @flow
import React from "react";
import styled from "typed-css";

const StyledComponent = styled.div`
    display: flex;
    height: 60px;
`.withModifiers({
    active: `
        background: red;
    `,
    disabled: `
        opacity: 0.5
    `
});
```

#### Using
```javascript
<StyledComponent modifiers="active" />
```
Multiple modifiers:
```javascript
<StyledComponent modifiers={["active", "disabled"]} />
```
Non declared specifier will throw typing error:
```javascript
// TypeError: field 'foo' is not declared
<StyledComponent modifiers="foo" />
```

#### Output code
```css
.StyledComponent-df5234f {
    display: flex;
    height: 60px;
}
.StyledComponent--active-45df53 {
    background: red;
}
.StyledComponent--disabled-j84jje {
    opacity: 0.5;
}
```

## Dynamic props
```javascript
// @flow
import React from "react";
import styled from "typed-css";

const StyledComponent = styled.div`
    display: flex;
    height: 60px;
`.withDynamicProps({
    image: (image: string) => `
        background: url(${image});
    `
});
```

#### Using
```javascript
<StyledComponent image={"./picture.jpg"} />
```
#### Output code
```css
:root {
    --StyledComponent--image-xg3r6gr: "./picture.jpg"
}
.StyledComponent-df5234f {
    display: flex;
    height: 60px;
    background: url(var(--StyledComponent--image-xg3r6gr));
}
```
TODO: var binded to component, that used styled component.

## Referring

```javascript
const OtherComponent = styled.div`
    ${StyledComponent.active}:hover & {
        color: white;
    }
`; 
```

#### Output code
```css
.StyledComponent--active-45df53:hover .OtherComponent-rt56pl6 {
    color: white;
}
```
