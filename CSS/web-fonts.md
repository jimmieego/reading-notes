## The `@font-face` rule

This rule sets the name and type of the font and provides the browser with the location of the file to use. 

```css
@font-face {
	font-family: FontName;
	src: local('fontname'), url('/path/filename.otf') format('opentype');
}
@font-face {
	font-family: FontName;
	font-style: italic;
	src: url('/path/filename.otf') format('opentype');
}
```

To use the font:

```css
h2 {
	font-family: FontName;
}
```

The italic style will be applied automatically without having to define it in the CSS for `<em>` element.

You can define any number of variations of a font with this method by using different font properties in the `@font-face` rule: `font-weight` to set various weights, `font-variant` for small caps faces, and so on.

## A "Bulletproof" Syntax

```css
@font-face {
	font-family: 'Gentium Basic';
􏰀 	src: url('GenBkBasR.eot'); /* For IE 8 and below */
􏰁 	src: url('GenBasR.eot?#iefix') format('embedded-opentype'), 􏰂 /* For IE 9 compatibility */
	url('GenBkBasR.woff') format('woff'), 
	url('GenBkBasR.ttf') format('truetype');
}
```

Tool: [Webfont Generator](https://www.fontsquirrel.com/tools/webfont-generator) by Font Squirrel

Note: 
- WOFF is a web-only format and can contain licensing information.
- The best policy is to check that the font you choose has a license explicitly allowing you to use it for web embedding.