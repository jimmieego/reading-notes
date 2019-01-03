## Selectors

CSS selectors define the elements to which a set of CSS rules apply.

[MDN: CSS selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)

## Inheritance and the cascade

[MDN: The Cascade and Inheritance](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Cascade_and_inheritance)

## The box model

The standard CSS Box Model (`box-sizing: content-box;`) takes the width that you have given an element, then adds onto that width the padding and border — meaning that the space taken up by the element is larger than the width you gave it.

`box-sizing: border-box;` uses the given width on the element as the width of the visible element on screen. Any padding or border will inset the content of the box from the edges.

To globally use the border-box model:

```css
html {
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
}
```

## Normal flow

Block Flow Layout. Start with a correctly marked up HTML document.

## Formatting contexts

Formatting contexts essentially define an outer and an inner type. The outer controls how the element behaves alongside other elements on the page, the inner controls how the children should look.

For example, `display: flex;` sets the outer to be a block formatting context, and the children to have a flex formatting context.

## Being in or out of flow

Elements in CSS are described as being ‘in flow’ or ‘out of flow.’ Elements in flow are given space and that space is respected by the other elements in flow. If you take an element out of flow, by floating or positioning it, then the space for that element will no longer be respected by other in flow items.

`position: absolute;` make sure you don't have overlapping content.

Floated items are also removed from flow. While following content will wrap around the shortened line boxes of a floated element, if you set a background color to the following elements, the background color will overlap with the floated item.

[MDN: In Flow and Out of Flow](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flow_Layout/In_Flow_and_Out_of_Flow)

## Alignment

[MDN: CSS Box Alignment](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Alignment)

## Sizing

[Sizing in Layout](https://www.smashingmagazine.com/2018/01/understanding-sizing-css-layout/)

## Responsive design

[Using Media Queries For Responsive Design In 2018](https://www.smashingmagazine.com/2018/02/media-queries-responsive-design-2018/)

## Fonts and typography

## Transforms and animation

[MDN: Using CSS Transforms](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transforms/Using_CSS_transforms)

[MDN: Using CSS Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations)