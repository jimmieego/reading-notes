## The `@font-face` rule

This rule sets the name and type of the font and provides the browser with the location of the file to use. 

```css
@font-face {
	font-family: FontName;
	src: local('fontname'), url('/path/filename.otf') format('opentype');
}
```

To use the font:

```css
span {
	font-family: FontName;
}
```

