# Design for Hackers: Reverse-Engineering Beauty

David Kadavy

## Introduction

- The world is in need of design literacy.
- A hacker values knowledge and learns whatever he needs to learn to achieve his vision.
- There really is a thought process - a decision-making framework - behind design.

## Chapter 1. Why Design Matters

The layers of design: purpose, medium and technology, and aesthetic decisions.

## Chapter 2. The Purpose of Design

You don’t always need a great visual design to be successful. Be sensitive to the needs of your users, how they interact with your product, and how your product fits into the competitive landscape.

Great visual design depends upon great user experience design. Use some form of a user experience design process early on in your project. User personas, use cases, and wireframes all help you focus on the critical aspects of user experience before getting caught up in details.

## Chapter 3. Medium and Form in Typography

Evenness of weight, or *texture*, is important to the legibility and readability of typography.

*Letterfit* is the consideration given to the letterforms to allow them to be set together in an even manner.

*Kerning* is the distance between two letters, and good fonts have parameters (or *kerning tables*) set for just about every letter combination in which the font may eventually be set.

> (On Page 51) The end of a brush stroke, if the brush is simply lifted, looks awkward, so serifs were added to the letters to give them a clean look and enhance readability.

> In some Roman inscriptions, it’s likely that the chisel was the source of the serif.

The theoretical underpinnings of Roman capitals: the square, the circle, and the triangle.

Notable letters of typographic history:

- Square capitals: influenced by the pen with which they are created
- Rustic capitals: more condensed than square capitals are, and the letters are simplified a bit.
- Trajan’s Column: the letters follow the basic shapes of the square, triangle, and circle, with great consideration given to the balance between the letters themselves and the negative spaces within and between the letters.
- Half uncials
- Carolingian minuscule: the birth of what we today consider “lowercase”.
- Textura
- Gutenberg
- Jenson
- Garamond: one of the most readable typefaces available for printed media.
- Baskerville
- Bodoni: Where the strokes sharply go from thick to thin, they’re rounded with geometric precision. The self-consciousness of this typeface’s design makes it perfect for the many fashion magazines in which it is commonly used.
- Slab-serif
- Sans-serif
- Decorative type
- Art Nouveau
- Futura
- Helvetica
- Chicago: its letters are mostly composed of heavy vertical strokes that are easily rendered with pixels
- Adobe Garamond
- Georgia: arguably the most readable serif font for web use.
- Arial: arguably the most readable sans-serif font for web use.

If you were looking for an alternative to Garamond for use on the web, you’d find no better choice than Georgia. The larger x-height of Georgia makes it more readable on-screen.

Today’s screens are incompatible with subtle curvilinear form like in Garamond.

The only way for a designer or developer to ensure that she’s making the right font choice is for her to develop an understanding of the font’s intentions and the limitations of the screen technology – or whatever medium in which the design will finally be conveyed.

- Learn about the different types of typefaces, paying special attention to who designed them and how technology influenced the design.
- On today’s screens (about 100 ppi to 150 ppi), stick with web-standard fonts at sizes below 30 px.
- Feel free to use custom fonts from Typekit, Cufón, or other technologies at sizes above 30 px, but be sure that you understand the font and how best to pair it.
- Avoid using fonts designed for the screen in print applications.

## Chapter 4. Technology and Culture

Neoclassical art usually depicted scenes from ancient Greek or Roman history or mythology, painted as realistically as possible.

Avoid simply copying a graphic style, and try to understand its technological and cultural influences.

## Chapter 5. Fool’s Golden Ratio: Understanding Proportions

*Proportion* is how the size or magnitude of one thing relates to that of another related thing.

Proportional relationships help organize the various elements involved in a design, not only drawing the attention of the viewer, but guiding her eye throughout that piece of design.

Well-considered geometric relationships help make a composition interesting.

## Chapter 6. Holding the Eye: Composition and Design Principles

The term *composition* refers to the way that elements are arranged within a piece of design, the interrelationships between those elements, and – if applicable – the relationships between those elements and a canvas or display.

### Foreground/background relationships

Size, color, texture, and use of shadows are just some of the factors that can make some things pop, while others recede.

### Design principles

Dominance: The principle of dominance creates visual interest in a composition by drawing the viewer’s eye to an important element in the composition.

Similarity: Similarity means that various elements of a composition – their shape, color, line characteristics (smooth or jagged), or texture – are similar to one another. Similarity makes a design look cohesive, because the various elements within it echo one another.

Rhythm: The repetition of a particular design element or characteristic throughout a composition create a sense of rhythm in design.

Texture: Texture is the visual indication that something has characteristics that would be palpable if you were able to touch them.

Direction: The principle of direction helps guide the viewer’s eye throughout the composition and helps keep the viewer looking at the design piece.

Contrast: The principle of contrast causes certain parts of a composition to stand out more than others because of differences – or contrast – between elements.

## Chapter 7. Enlivening Information: Establishing a Visual Hierarchy

A piece of information with lots of white space around it will often look more important than other information. Simply considering the amount of white space used between elements, and being consistent, can go a long way toward making a design look more clean.

It’s good practice to pick some proportional scale of type sizes to work with. For example: 5, 7, 9, 12, 16, 21, 28, 37, 50, 67. (The scale factor is 0.75.)

## Chapter 8. Color Science

### Color and quantitative data

When choosing a color palette to express quantitative data, you need to understand how different color shifts – within various color models – differ perceptually. The data representations of color that are present in popular color spaces don’t always translate to equivalent perceptual differences in the colors produced.

For example, the Lightness value in HSL – like the Brightness value in HSB – isn’t consistent with actual human perception.

[Colorbrewer](http://www.colorbrewer2) makes it easy to create color palettes that are perceptually distinct.

A *diverging color palette* places two concentrated hues, each at its own extreme ends of the data, and fade those hues into a neutral color for data that is around the data point that is neutral (such as the median).

Use colors with a consistent perceptual lightness for qualitative data sets, and color palettes with appropriately perceptually contrasting lightness for quantitative data sets.

### Hexadecimal color

To know how to mentally navigate through the hexadecimal color cube in a 256-color palette, you need to remember only this progression: `0`, `3`, `6`, `9`, `C`, `F`.

### HSL

HSL: Hue, Saturation, Lightness.

Hue: 0 - 360. Saturation and lightness are in percentages.

In HSL, any color with 100 percent Lightness will simply be white, and *50 percent* is designated for pure hues.

### Color across media

When working with an RGB image, make sure to work within the sRGB color space, so the image’s colors can be interpreted across a wide variety of devices. Don’t attach an ICC profile to web graphics that you need to match with CSS colors.

## Chapter 9. Color Theory

- Use red in contexts where you want to drive user behavior forward.
- Use red in error messages and other urgent notes.
- Consider using red if you're doing any work related to food. Avoid strong use of blue in these contexts.
- Avoid red in performance-based contexts.

### Artist's color wheel

*Primary colors*: Red, Yellow, Blue

*Secondary colors*: Orange (Red + Yellow), Green (Yellow + Blue), Purple (Blue + Red)

*Tertiary colors*: Mix one of the primary colors with the adjacent secondary color.

### Color choices and web conventions

#### Backgrounds

White: A white background, when used with dark type, provides good contrast for reading and conveys a sense of trustworthiness. The more widespread the audience of a website, the more likely it is to have a white background.

Off-white: Off-white or cream colors often are associated with things that have a natural feel to them. Additionally, off-white or cream gives a stronger sense of intimacy than does pure white. Off- white gives a sense of antiqueness, too, like paper that is old and has started to yellow.

Dark: Dark backgrounds can provide a sense of exclusivity and sophistication.

Bright: If you choose to use a brightly colored background, make sure it’s relevant. Bright background may not be suitable for reading a lot of content on the page.

#### Graphics and text

Green: A mark of progress. Call-to-action buttons.

Yellow: Call attention to important messages or notes.

Red: Error or other urgent message that's critical for the user to see.

Blue: Link color.

#### Accent colors

The color needs to contrast with its surroundings.

### Color theory

As a general rule, warm hues pop out at the viewer, giving the appearance of being closer, while cool hues recede, giving the appearance of being farther away.

A tint of a hue is basically a lighter version of that hue. A shade is a darker version of the base hue. Tints pop and shades recede.

By understanding how colors interact with one another, you can more strongly establish a hierarchy of information in your typography. Web conventions have made it widely acceptable to use black on white for text on web pages, but this isn’t universally the most readable, nor is it the most aesthetically pleasing option.

Example:

Main text color: `#503e2b`. Secondary text color: `#808094`.

Don’t be so quick to use black – if you really master manipulating color relationships to create dimension, you can really add freshness and life to your designs.

### Color schemes

#### Monochromatic

A monochromatic color scheme uses a single base hue - usually with varied tints and shades of that hue - throughout the design.

#### Analogous

Analogous color schemes typically use three hues that are adjacent to each other on the color wheel (for example, green-blue, green, and green-yellow), though sometimes an intermediate color may be skipped between colors (for example, blue, green, yellow). Analogous color schemes tend to be harmonious and quiet.

#### Complementary

Complementary color schemes are made up primarily of two colors that are opposite each other on the color wheel. Complementary colors contrast with each other as much as possible, so these color schemes tend to have an exciting, jarring appearance.

#### Split-complementary

A split-complementary color scheme is made up of a color and the two colors that are on either side of the complement of that color. Split-complementary color schemes tend to feel less jarring and more harmonious than complementary color schemes.

#### Triadic

A triadic color scheme is composed of three colors that are evenly spaced on the color wheel.

#### Tetradic

A tetradic color scheme is composed of two pairs of complementary colors, for a total of four colors.

### Creating a mood with color

Mysterious or exclusive: Designs that have a sense of mystery or exclusivity tend to have a very dark overall feeling to them, possibly with some sparse but bright highlights or accent colors.

Active: Designs that feel active tend to have bright and highly saturated colors that contrast each other.

Calm: Designs with a muted palette have a very quiet, often calming feeling. Muted color palettes generally consist of very unsaturated tints of colors – mostly grays, beiges, or even subtle pastels.

Muted: Muted color palettes are often a good setup for increasing the impact of accent colors.

Natural: Natural color palettes have an earthy feeling that reminds you of a hike through the woods. Usually, greens, browns, brownish-orange, and brownish-yellow colors are seen in designs that have a “natural” feeling.

### Key points

- When working with predefined color palettes, use accents to your advantage. Just pick one or two colors to dominate your color usage, and use the others sparingly to add accents to particular elements you want to call attention to.
- When designing for an unfamiliar culture, do your research. Make sure you aren’t bringing to mind any dominant cultural elements, such as religion or death, unless you intend to.
- Use your knowledge about how colors interact (for example, cool colors recede while warm colors pop) to add extra life and dimension to your designs.
- Use your knowledge of some of the common signals that colors carry with them (for example, yellow for bonus information) to guide your color choices in appropriate contexts.

## Appendix A. Choosing and Pairing Fonts

### Humanist typefaces

Very readable on-screen.

- Gill Sans: friendly and approachable.
- Lucida Grande
- Verdana
- Tahoma
- Trebuchet MS

### Geometric typefaces

More directly influenced by the square, circle, and triangle. The `o`’s of geometric typefaces tend to be nearly perfect circles.

- Futura: simple yet sophisticated.
- Bodoni

### Realist/Transitional typefaces

A balance between calligraphic and geometric influence.

- Helvetica
- Georgia
- Times New Roman: A major consideration in the 1931 design of Times New Roman was to save space in the British newspaper, *The Times*.

### Pairing fonts

Use no more than two fonts: one of them serif, and one sans-serif.

In print, if two fonts are being used, a sans-serif face is typically used for titles and headers, while a serif face is used for body copy.

Sans-serif typefaces are regarded as more readable on-screen, so when a second font is used, it’s often a serif typeface for more sophisticated-looking headers and titles.

The reverse of this common configuration – a sans-serif font for headers and titles, with a serif font for body copy – is certainly a viable option, provided that the serif face is one designed for the web (such as Georgia) and is displayed large enough to be readable.

When pairing fonts, it’s best to achieve *harmony* or *contrast*. It’s the area in between these two approaches that you want to avoid.

A good shortcut is to choose fonts that are created by the same type designer (e.g., Joanna and Gill Sans by Eric Gill).

### Font

As a good rule of thumb, body copy tends to be most readable when the leading is about 120 percent to 140 percent of the type size (a `line-height` of `1.2em` to `1.4em`). Smaller portions of text, such as within bulleted lists, tend to look better with a smaller `line-height` (`1em` or `1.1em`).

## Appendix B. Typographic Etiquette

