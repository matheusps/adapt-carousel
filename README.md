# Adapt Carousel

Some short description

## Installing

Simple install it as a module

```bash
$ yarn add adapt-carousel
```

or

```bash
$ npm install adapt-carousel
```

### Basic

The simplistic way of using `Adapt Carousel` is:

```typescript
import React from 'react'
import { Carousel } from 'adapt-carousel'

const YourComponent: React.FC = () => {
  return (
    <Carousel>
      <img src="url1" />
      <img src="url2" />
      <img src="url3" />
      <img src="url4" />
    </Carousel>
  )
}
```

### Resposive

The `elements` prop will specify how many items will be presented on each breakpoint (`visible`) and how many elements will be passed each type (`toPass`). The `elements` object has the type:

```typescript
interface responsiveType {
  /** key is the type name such as mobile, desktop, tablet, ... */
  [key: string]: {
    breakpoint: { max: number; min: number }
    items: number
  }
}

interface SliderProps {
  /** Element props */
  elements: {
    /** Number of visible elements per breakpoint */
    visible: responsiveType
    /** Number of elements that are passed each time 1 to visible */
    toPass?: number | 'visible'
  }
}
```

So, on your component you will use it like:

```javascript
import { Carousel } from 'adapt-carousel'
import Image from './Image'

const visibleElements = {
  desktop: {
    breakpoint: { max: 3000, min: 1024 },
    items: 4,
  },
  tablet: {
    // ...
  },
  mobile: {
    // ...
  },
}

const slides = [
  { url: '...' },
  // ...
]

<Carousel
  elements={{
    visible: visibleElements,
    toPass: 'visible' // will pass every visible element each arrow click
  }}
>
  { slides.map(slide => <Image {...slide} />) }
</Carousel>
```

### Configuration

| Prop name                 | Type                  | isRequired | defaultValue     | Description                                     |
| ------------------------- | --------------------- | ---------- | ---------------- | ----------------------------------------------- |
| `label`                   | `String`              | 🚫         | 'Adapt Carousel' | Aria label of slider                            |
| `deviceType`              | `String`              | 🚫         | 🚫               | The device type                                 |
| `elements`                | `SliderElements`      | ✅         | -                | Elements props                                  |
| `children`                | `Array<Node!>`        | ✅         | 🚫               | Elements to render                              |
| `showArrows`              | `Boolean`             | 🚫         | true             | If should show arrows                           |
| `showDots`                | `Boolean`             | 🚫         | true             | If should show dots                             |
| `removeArrowOnDeviceType` | `Array<String!>`      | 🚫         | 🚫               | Which device types that arrows should be hidden |
| `customLeftArrow`         | `ComponentType<any>!` | 🚫         | 🚫               | Custom arrow on left                            |
| `customRightArrow`        | `ComponentType<any>!` | 🚫         | 🚫               | Custom arrow on right                           |
| `customDot`               | `ComponentType<any>!` | 🚫         | 🚫               | Custom dots                                     |
| `infinite`                | `Boolean`             | 🚫         | true             | Whatever is infinite mode or not                |
| `classNames`              | `ClassNames`          | 🚫         | -                | Custom classes                                  |
| `thumbnails`              | `Thumbnails`          | 🚫         | -                | Props for thumbnails                            |
| `autoplay`                | `AutoplayProps`       | 🚫         | -                | Props for autoplay                              |
| `keyboardControlled`      | `Boolean`             | 🚫         | false            | If is controlled via keyboard arrows or not     |

**SliderElements Type**

| Prop name | Type                 | isRequired | defaultValue                                            | Description                                               |
| --------- | -------------------- | ---------- | ------------------------------------------------------- | --------------------------------------------------------- |
| `visible` | `responsiveType`     | ✅         | `every: { breakpoint: { max: 3840, min: 0 }, items: 1}` | Number of visible elements per breakpoint                 |
| `toPass`  | `Number | 'visible'` | 🚫         | 1                                                       | Number of elements that are passed each time 1 to visible |

**ClassNames Type**

| Prop name           | Type     | isRequired | defaultValue | Description                                  |
| ------------------- | -------- | ---------- | ------------ | -------------------------------------------- |
| `slider`            | `String` | 🚫         | `''`         | Custom classes for slider                    |
| `container`         | `String` | 🚫         | `''`         | Custom classes for container                 |
| `item`              | `String` | 🚫         | `''`         | Custom classes for item                      |
| `leftArrow`         | `String` | 🚫         | `''`         | Custom classes for left arrow                |
| `rightArrow`        | `String` | 🚫         | `''`         | Custom classes for right arrow               |
| `dotList`           | `String` | 🚫         | `''`         | Custom classes for the dot list              |
| `dot`               | `String` | 🚫         | `''`         | Custom classes for a single dot              |
| `thumbnails`        | `String` | 🚫         | `''`         | Custom classes for the thumb container       |
| `thumbnail`         | `String` | 🚫         | `''`         | Custom classes for all single thumbs         |
| `selectedThumbnail` | `String` | 🚫         | `''`         | Custom classes for the selected single thumb |

**Thumbnails Props**

| Prop name  | Type               | isRequired | defaultValue | Description                                        |
| ---------- | ------------------ | ---------- | ------------ | -------------------------------------------------- |
| `items`    | `Array<Thumbnail>` | ✅         | 🚫           | Array of thumbnails                                |
| `position` | `'left' | 'right'` | ✅         | 🚫           | Thumbs position relative to slider container       |
| `width`    | `String`           | ✅         | 🚫           | Thumbs width measure can be `rem`, `px`, `%`, etc. |

**Thumbnail Type**

| Prop name  | Type     | isRequired | defaultValue | Description                   |
| ---------- | -------- | ---------- | ------------ | ----------------------------- |
| `url`      | `String` | ✅         | 🚫           | Url of the thumbnail          |
| `forSlide` | `Number` | ✅         | 🚫           | Slide index that it refers to |

**Autoplay Props**

| Prop name     | Type      | isRequired | defaultValue | Description                                      |
| ------------- | --------- | ---------- | ------------ | ------------------------------------------------ |
| `timeout`     | `Number`  | ✅         | 🚫           | Time duration in ms                              |
| `stopOnHover` | `Boolean` | 🚫         | 🚫           | If should stop the timeout by hovering the slide |
