# three-n2h

<a href="https://www.npmjs.com/package/three-n2h" target="_blank" rel="noopener noreferrer"><img src="https://badgen.net/npm/v/three-n2h" alt="NPM Version" /></a>
<a href="https://www.npmjs.com/package/three-n2h" target="_blank" rel="noopener noreferrer"><img src="https://badgen.net/npm/dt/three-n2h" alt="NPM Downloads" /></a>
<a href="https://github.com/alexzhang1030/three-n2h/blob/main/LICENSE" target="_blank" rel="noopener noreferrer"><img src="https://badgen.net/github/license/alexzhang1030/three-n2h" alt="License" /></a>

Three.js nice to have things, kinda like a supplement to [`@pmndrs/vanilla`](https://github.com/pmndrs/drei-vanilla)

## Installation

```bash
pnpm i three-n2h
```

## Things

### Text

[drei counterpart](https://drei.docs.pmnd.rs/abstractions/text#text)

Hi-quality text rendering w/ signed distance fields (SDF) and antialiasing, using [troika-3d-text](https://github.com/protectwise/troika/tree/master/packages/troika-3d-text). All of troikas props are valid!

> Required `troika-three-text` >= `0.46.4`

```ts
export interface TextProps {
  characters?: string
  color?: number | string
  // the text content
  text: string
  /** Font size, default: 1 */
  fontSize?: number
  maxWidth?: number
  lineHeight?: number
  letterSpacing?: number
  textAlign?: 'left' | 'right' | 'center' | 'justify'
  font?: string
  anchorX?: number | 'left' | 'center' | 'right'
  anchorY?: number | 'top' | 'top-baseline' | 'middle' | 'bottom-baseline' | 'bottom'
  clipRect?: [number, number, number, number]
  depthOffset?: number
  direction?: 'auto' | 'ltr' | 'rtl'
  overflowWrap?: 'normal' | 'break-word'
  whiteSpace?: 'normal' | 'overflowWrap' | 'nowrap'
  outlineWidth?: number | string
  outlineOffsetX?: number | string
  outlineOffsetY?: number | string
  outlineBlur?: number | string
  outlineColor?: number | string
  outlineOpacity?: number
  strokeWidth?: number | string
  strokeColor?: number | string
  strokeOpacity?: number
  fillOpacity?: number
  sdfGlyphSize?: number
  debugSDF?: boolean
  onSync?: (troika: any) => void
  onPreloadEnd?: () => void
}
```

Usage

```jsx
const text = Text({
  text: 'Hello World',
})
const mesh = new THREE.Mesh(geometry, material)
mesh.add(text.mesh)
```

Text function returns the following

```ts
export interface TextType {
  mesh: THREE.Mesh
  updateProps: (newProps: Partial<TextProps>) => void
  dispose: () => void
}
```

You can preload the font and characters:

```ts
const preloadRelatedParams = {
  // support ttf/otf/woff(woff2 is not supported)
  font: '/your/font/path',
  characters: 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890!?.,:;\'"()[]{}<>|/@\\^$-%+=#_&~*',
  onPreloadEnd: () => {
    // this is the callback when font and characters are loaded
  },
}
```

## License

MIT
