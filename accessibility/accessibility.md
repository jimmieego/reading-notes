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