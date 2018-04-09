# Responsible Responsive Design

Scott Jehl

## Introduction

A responsible responsive design equally considers the following throughout a project:

- **Usability**: The way a website’s user interface is presented to the user, and how that UI responds to browsing conditions and user interactions.
- **Access**: The ability for users of all devices, browsers, and as- sistive technologies to access and understand a site’s features and content.
- **Sustainability**: The ability for the technology driving a site or application to work for devices that exist today and to continue to be usable and accessible to users, devices, and browsers in the future.
- **Performance**: The speed at which a site’s features and content are perceived to be delivered to the user and the efficiency with which they operate within the user interface.

## Responsible Design

Responsive design's core tenets: fluid grids, fluid images, and media queries.

Two responsible tenets: **usability** and **accessibility**.

The number of characters per line in a column of text for immersive reading is widely thought to fall between **45** and **75** characters, including spaces.

It is often helpful to compile the multiple configurations of each modular components in isolation, in order to test its usability and document its variations in one place.

### Progressive disclosure

Hide portions of content, but provide interface cues so that users can view it when they wish.

### Responsive table

- Reflow the table from a multile-column view to a list view; each cell becomes its own row, with a row header to its left. This pattern falls short when you need to compare data points across rows.
- Horizontal scrolling and allow the user to show/hide columns.

### Touch

- Make sure any content that offers mouse-centric interactivity (like `hover`) is also accessible in browsers where a mouse pointer may not exist.
- Don't assume touch will be used, but design as if it will be.
  - Apple suggests 44 x 44 px as the minimum size for usable buttons.
- Ensure there's always a click-and-keyboard-based interface for interaction. Think of touch gestures as a nice-to-have enhancement on top of broadly supported input modes.

## Sustainable Detection

**Features**: CSS properties and JavaScript APIs
**Constraints**: Viewport size, unpredictable connectivity, off-line use

Designing for features and constraints allows us to see how patterns that may otherwise seem distinct are shared across devices, and to build in a modular manner to create unique experiences that feel appropriate to each device.

**Mobile first**: Start small and layer in more complex layout as space permits. This helps prioritize content.

A mobile-first responsive stylesheet begins with styles that are shared across all experiences, forming the foundation of the smallest screen layout. These styles are followed by a series of mostly `min-width` media queries to scale that layout up to greater viewport sizes and pixel depths.