# Vue Picture Sharesheet Compoenent
![image](https://thumbs.gfycat.com/KindSourHammerkop-size_restricted.gif)

## [Demo](https://onatcer.github.io/vue-picture-sharesheet/) 😻
with cute cats 😻
(The Download in the Demo will just download random cat images as the image changes with every request)

## Getting Started
*(Vue CLI Usage recommended)*

Install
```shell
npm install vue-picture-sharesheet --save
```

Import locally
```javascript
import PictureSharesheet  from 'vue-picture-sharesheet';

export default {
  name: 'HelloWorld',
  components: {
    PictureSharesheet
  }
}
```

OR import globally (f.e. in the Main.js)
```javascript
import PictureSharesheet from 'vue-picture-sharesheet'
Vue.component('picture-sharesheet',PictureSharesheet);
```



## Properties
### Native image attributes 🛠
  - `src`: String : URL, Specifies the URL of an image
  - `alt`: String : text, Specifies an alternate text for an image
  - `height`: String : pixels/%, Specifies the height of an image
  - `width`: String : pixels/%, Specifies the width of an image
  - `ismap`: boolean : ismap, Specifies an image as a server-side image-map
  - `longdesc`: String : URL, Specifies a URL to a detailed description of an image
  - `usemap`: String : #mapname, Specifies an image as a client-side image-map
  - `crossorigin` : String:  anonymous | use-credentials, Allow images from third-party sites that allow cross-origin access to be used with canvas

### Component attributes 🎨
  - `sheetcolor`: String : Color, Specifies the Background-color of the Sharesheet
  - `iconcolor`: String : Color, Specifies the Background-color of the Sharesheet
  - `position`: String : bottom | top | left| right, Position of the Sharesheet
  - `size`: String : pixels/%, height/width of the Sharesheet
  - `sharemessage`: String : Will be shared in addition to the link. Per Default Website Title. In Facebook Share Dialog as Quote.
  - `fixed`: Boolean : if set Sharesheet is visible all the time

## Examples

Showing the Sharesheet all the time (not only while :hover) and set the background-color of the sharesheet to white and the icon color to black.
```javascript
<picture-sharesheet src="https://source.unsplash.com/800x500/?cat" sheetcolor="#FFF" iconcolor="#000" fixed/>
```

Set the position of the sharesheet to top, the height of the Sharesheet to 100px and the message that will be shared via the Social Media Buttons to "YAY!"
```javascript
<picture-sharesheet src="https://source.unsplash.com/600x550/?cat" position="top" size="100px" sharemessage="YAY!"/>
```

## Commands
- `npm start` - Starting a Server to run the demos/examples
- `npm run-script demo` - Building the demos/examples in /docs

<!---
## Commands from the Boilerplate
- `npm run clean` - Remove `lib/` directory
- `npm test` - Run tests with linting and coverage results.
- `npm test:only` - Run tests without linting or coverage.
- `npm test:watch` - You can even re-run tests on file changes!
- `npm test:prod` - Run tests with minified code.
- `npm run test:examples` - Test written examples on pure JS for better understanding module usage.
- `npm run lint` - Run ESlint with airbnb-config
- `npm run cover` - Get coverage report for your code.
- `npm run build` - Babel will transpile ES6 => ES5 and minify the code.
- `npm run prepublish` - Hook for npm. Do all the checks before publishing your module.
-->
## Roadmap
- [ ] Multiple Image Source (srcset .. )
- [ ] Mobile optimized
- [ ] different overlay modes
- [ ] custom icons


