<!-- SvgSprite.vue -->

<template>
  <svg width="0" height="0" style="display: none;" v-html="$options.svgSprite" />
</template>

<script>
const svgContext = require.context(
  '!svg-inline-loader?' + 
  'removeTags=true' + // remove title tags, etc.
  '!@/../assets/icons', // search this directory
  true, // search subdirectories
  /\w+\.svg$/i // only include SVG files
)
const symbols = svgContext.keys().map(path => {
  // get SVG file content
  const content = svgContext(path)
   // extract icon id from filename
  const id = path.replace(/^\.\/(.*)\.\w+$/, '$1')
  // replace svg tags with symbol tags and id attribute
  return content.replace('<svg', `<symbol id="${id}"`).replace('svg>', 'symbol>')
})
export default {
  name: 'MapSvgSpriteColor',
  svgContext: svgContext,
  svgSprite: symbols.join('\n'), // concatenate all symbols into $options.svgSprite
}
</script>