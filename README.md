# vue-image-viewer-component
Vue.js component of image viewer using [v-viewer](https://github.com/mirari/v-viewer)

## Installation

```bash
npm i castling/vue-image-viewer-component
```

## Usage:

```javascript
import ImageViewer from 'castling/vue-image-viewer-component'

Vue.comonent('image-viewer', ImageViewer)
```

# props

* `images` `{Array<String>}` image URLs
* `page` `{Number}` showing page number [sync]
