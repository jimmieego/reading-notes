## Headings
https://www.nomensa.com/blog/2017/how-structure-headings-web-accessibility

Heading 1 is the most important and is the heading for the page, this typically corresponds to the title of the page. It gives users an indication of what the page is about - you should have a single Heading 1 on each page.

Each heading 2 creates a **section** of content. They divide pages into consumable sections which help to organize the content.

When a section is visually obvious you can hide headings from sighted users.

- Don’t style text to look like a heading unless you use heading mark-up.
- The level of heading is not the same as the text size.

## Reporting accessibility issues
https://medium.com/@ckundo/6-tenets-of-accessibility-bug-reporting-cdfed82af0b8

- Focus on Conversions: Focus remediation on user journeys that lead to conversion.. For example, if your customer can’t complete a purchase, they’ll be more frustrated than (for a screen reader user) a poorly described image on the home page. You’re also more likely to get buy-in from product managers and leadership when you focus on conversion.
- Describe Human Impact: Describe an issue’s impact in human terms. Include customer feedback if you can.
- Let Teams Prioritize: Give teams the information they need, then trust them to be professional and organized.
- Recommend Solutions: Give technical guidance, but avoid prescribing solutions.
- Attention, not Assignment: Bring attention to an issue, then let teams decide how to assign.

## Accessibility tree
https://developer.paciellogroup.com/blog/2018/03/short-note-on-what-css-display-properties-do-to-table-semantics/

Screen readers and other assistive tech, in general, do not have direct access to the HTML DOM, they are provided access to a subset of information in the HTML DOM via [Accessibility APIs](https://www.w3.org/TR/wai-aria-1.1/#dfn-accessibility-api). Sometimes what an element represents in the HTML DOM is not how it is represented in the accessibility tree.

## `Title`
In the case of a search input, there’s typically a magnifying glass as an icon within the input. The pattern is so common that the location and the icon are typically the only references a sighted user needs to understand the purpose of the input. Instead of forcing a visually hidden label, or utilizing an `aria-label` to announce the accessible name of the input, use a `title="Search site/app"` instead. You’ll get a free tooltip for sighted users, and the accessible name you need for screen readers.

### Using `title` on `abbr` elements

Example:

```html
<p>
  Again, the <abbr title="World Wide Web Consortium">W3C</abbr>...
</p>
```

### Using `title` on `iframes`

Using a `title` on an `iframe` is actually important to meet WCAG success criteria, as this is a recommended way to give an accessible name to frames, using the native HTML language alone. For example: `<iframe src="url_here" title="the title of a website">`.