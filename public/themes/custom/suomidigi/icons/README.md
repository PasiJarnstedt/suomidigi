## How to convert the icons to sprite

Add your new icon to ./svg/ folder.

In theme folder /themes/custom/suomidigi/ run
 
    npm run generate-svg-sprite
    
## Usage

HTML:
```
<svg class="icon">
  <use xlink:href="#alert" />
</svg>

<svg class="icon">
  <use xlink:href="#download" />
</svg>
```

See: https://css-tricks.com/svg-symbol-good-choice-icons/
