# Style = Substance

Translating Good Design into Great Accessibility

- Amelia Bellamy-Royds
  - Author & Web Standards Editor
  - W3C Invited Expert, SVG and ARIA working groups
  - [@AmeliasBrain](https://twitter.com/settings/account)
  - amelia.bellamy.royds@gmail.com
  
- ID24 for Global Accessibility Awareness Day 2016
  - http://www.inclusivedesign24.org/
  - 01:00 UTC, 19 May 2016

## Bad Design is an Accessibility Problem

- Poor contrast
- Indistinguishable colors
- Illegible fonts
- Unnecessary motion
- Confusing interface patterns

## I'm not here to talk about <br/>Bad Design

## I'm here to talk about <br/>Good Design

## Good Design Can Enhance Accessibility <br/>_if_<br/>the Style is translated into Substance

## What is Style?

- Appearance
- Fashion
- Typography, color schemes, icons, layout, graphical effects, animation
- Pretty much everything you control with CSS

## What is Substance?

- Meaning
- Function
- Context
- Connections
- Pretty much everything you can specify in HTML (and ARIA)
- AKA "Semantics"

## Accessibility <br/>is all about <br/>Substance

## Accessibility <br/>tends to overlook <br/>Style

## Making the Connection

- Many more visual designers than accessibility experts
- Designers are experts in communicating semantics
    - Meaning
    - Function
    - Context
    - Connections
- Designers who can translate style into substance can help ensure that _all_ users get the best experience

## _Some_ User Experience <br/>=<br/> SUX

## How Can <br/>Style=Substance<br/>?

## Markup is for Computers

- Most users never see your HTML tags
- Most users don't know if it's `<div>` soup
- So how do they understand the semantics?

## Style is for (most) People

- Layout communicates structure
- Shape, borders, & shadows communicate function
- Color and icons communicate state
- Motion communicates relationships

## Visual Style <br/>_Represents_ <br/> Substance <br/> for Visual Users

## Style (Alone) is Unreliable

- Alternative color schemes
- Plain text layouts
- Screen readers
- Keyboard control
- Bad connection: no CSS/images

## Need Redundancy

- All information communicated via visual styles must also be expressed in markup 
    - text content
    - semantic HTML tags
    - ARIA attributes
- It's not enough that code recreates a visual design
- It needs to encode the _meaning_ behind the design choices
- Designers need to speak the language of HTML + ARIA

## Include Semantics with Designs

- Visual mock-ups sent to coders annotated using HTML/ARIA semantics
- Pattern libraries using semantic markup
- Maybe: use CSS tag/attribute selectors to enforce the connection

## Checklist

Created an awesome style guide or pattern library?  
Make sure it's implemented accessibly:

1. Complex layout → Reading Order
2. Page templates → Main elements
3. Components → Roles
4. Repeated components → Lists
5. Icons & images → Alt text
6. Changeable components → States
7. Associated components → Relationships
8. Text styles → Semantic HTML


## Design the Reading Order

### Why?

- Screen readers can only read one thing at a time
- Many other tools have limited layout options
- Two-dimensional layout is reduced to a linear reading order
- Keyboard tabindex moves focus to one element at a time

### What?

- Every page template needs a reading order for components
  - [Sample page wireframe image](images/Profilewireframe.png)  
    → [Credit: Rob Enslin via Flickr/Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Profilewireframe.png)
- Complex components need internal reading order
  - [Fully annotated page template](images/Profilewireframe-readingOrder-components.png)
- Page templates need order for components
  - [Fully annotated page template](images/Profilewireframe-readingOrder-page.png)
  - [More realistic complex page](images/CBC-CategoryPage-2016-05-18-small.png)  
    → [Source: CBC News Technology & Science category page](http://www.cbc.ca/news/technology)
- Especially important for interaction
  - Information before user input requests
  - Controls before controlled content
  - Options before submit buttons
  - [Even simple forms have complex reading order issues](https://codepen.io/login)  
    → [Source: CodePen login page](https://codepen.io/login)

### How?

- Make DOM order match reading order
- For float-based layouts, use wrapper `<div>` elements instead of changing DOM order
- Use same-page navigation links (and landmark roles) to allow jumping to content
- If this is not enough, use `aria-flowto="next-element-id"` to change reading order
- Use `aria-owns="virtual-child-elements"` to change the effective tree structure
  - Can create tree structures when elements can't have children, e.g. SVG
  - [SVG shape elements can be DOM siblings but semantic containers](images/MBostock-CirclePacking.svg)  
    → [Source: Mike Bostock's D3 Circle Packing demo](http://bl.ocks.org/mbostock/4063530)
- Remember: `aria-owns` and `aria-flowto` don't change tab order


## Every Page Needs a Main

- Page templates → Main elements

### Why?
  - Allows screen reader users to skip to content
  - With `nav`, most important landmark element
  
### What?
  - Find the unique content for this template
    - [single blog post](images/CBC-ArticlePage-2016-05-18-small.png)    
      → [Source: CBC News article](http://www.cbc.ca/news/technology/bob-mcdonald-search-for-habitable-planets-1.3579830)
    - [article list](images/CBC-CategoryPage-2016-05-18-small.png)    
      → [Source: CBC News category page](http://www.cbc.ca/news/technology)
    - [search results](images/CBC-SearchPage-2016-05-18-small.png)    
      → [Source: CBC News search page](http://www.cbc.ca/gsa/?q=web+accessibility&gns=SEARCH)
  - Why is someone at _this_ URL and not any other?
  
### How?
  - An HTML `<main>` element (preferred)
  - ARIA `role="main"` on a non-interactive element (e.g., `<div>`)
  - There is only one!
  
  
## Extra credit: Add more landmarks

- Once you've identified the `<main>`, what's left?
- The remaining content should also be grouped into [landmark roles](https://www.w3.org/TR/wai-aria-1.1/#landmark_roles)
- Web site header
  - `role="banner"` 
  - `<header>` outside `<main>` or `<article>`
- Web site footer
  - `role="contentinfo"` 
  - `<footer>` outside `<main>` or `<article>`
- Site navigation
  - `<nav>` 
  - `role="navigation"`
  - if more than 1 per page, give it a meaningful name with `aria-label`
- Site search (if not the main content of this page)
  - `role="search"` on a `<form>`
- Sidebars & other modules
  - `<aside>`, `role="complementary"` or `role="region"`
  - e.g., top headlines, weather report, twitter feed
  - give it a meaningful name with `aria-label`
  
  
  
## Every Component Needs a Role

- Components → Roles

### Why?
- Non-visual users can't see your styles
- If it's important enough to style, it has a role in your website
- Roles give context & explain functionality

### What?
- Anything interactive
  - [buttons & links](images/LonelyPlanet-socialButtons.png)
  - [form elements](images/LonelyPlanet-dropdown.png)
  - [alerts & dialogs](images/LonelyPlanet-alert.png)
  - [image carousels](images/LonelyPlanet-imageSlider.png)
  - [tooltips](images/LonelyPlanet-tooltip.png)
  - [breadcrumb links](images/LonelyPlanet-breadcrumbs.png)
  - [pagination links](images/LonelyPlanet-pagination.png)  
    → [Source: Lonely Planet Style Guide](http://rizzo.lonelyplanet.com/styleguide/ui-components)
- Any composite item that forms a meaningful unit
  - [forms](images/CodePen-form.png)
  - [dialogs](images/CodePen-dialogs.png)
  - [cards](images/CodePen-blogPostCard.png)
  - [collections of cards](images/CodePen-blogPostBlock.png)  
    → [Source: CodePen Design Patterns and Style Guide](http://codepen.io/guide/)
- Pretty much anything in your pattern library
  - [More pattern libraries & style guides](http://styleguides.io/examples.html)

### How?

- Use HTML elements with native roles
- Use the ARIA `role` attribute
- Don't add non-interactive roles to interactive elements!
- Be careful adding or changing interactive roles
  - must re-create usual keyboard interactions with script
  - use JS to add roles that require JS


## Extra credit: Give them names!

- A role is only halfway to accessibility
- Most roles require author-provided names
- Use native HTML naming mechanisms for native HTML elements
  - `<caption>`, `<figcaption>`, `<label>`
  - Note `<label>` only works on [labelable elements](https://www.w3.org/TR/html51/sec-forms.html#labelable-element)
- Use `aria-labelledby="other-element-id"` for other labelling elements
- Use `aria-label="name"` if there's no visible label

## A Set of Components is a List

- Repeated components → Lists

### Why?

- Non-visual users can't see at a glance how many repeats there are
- Screen readers announce # of elements in a list
- Each item is announced with name of list & 
- Can optionally provide fallback list styles if CSS fails

### What?

- Any repeated unit with more than ~3 repeats
  - search results
  - product listings
  - article archives
  - comments
- May be called cards, tiles, panels, items, grids, feed
- _Not_ sections & headings that make up an organized outline of continuous text

### How?

- Wrap list in `<ul>` or `<ol>` and items in `<li>`
  - fallback will be list styles
- Wrap list in `<div role="list">` and items in `<div role="listitem">`
  - fallback will be block layout
- _May_ group list items with `<div role="group">` (ARIA lists only)
  - Groups can only contain list items
  - Often easier to have nested lists or a heading-based outline with multiple short lists
- No other markup between list element and list item element
  - If other wrappers required for layout, use `role="presentation"` on the wrapper elements
- Giving the list element a short name helps (not required)
- Avoid re-purposing semantic elements & never re-purpose interactive elements
  - use `<li><a>...</a></li>`
  - not `<a role="listitem">...</a>`
  - Elements can only have one role at a time!
  
## Extra credit: Number Partial Lists

- If content of current page is only part of the list, need extra work
- For paged lists, use `aria-setsize` and `aria-posinset`
  - Both specified on _each_ `listitem` or `<li>`
  - `aria-posinset` starts at 1
  - Yes, set size will be the same for all. Still need to repeat it.
- If total set size is unknown, use `aria-setsize="-1"`
- _Only_ use set attributes when list in DOM is incomplete
  - browser can calculate them for most lists
  - don't risk messing it up
- For continuous feed (unknown set size, new entries at either end) use new roles `feed` instead of `list` and `article` instead of `listitem`



## Every Image Needs Some Text

- Icons & images → Alt text

### Why?
  - Provides meaning to screen reader users
  - Provides fallback to other users
  - If the icon has a meaning, name it!
  - If the image provides context, describe it!
  
### What?
  - Icons in buttons, badges, links, and more
  - Any other image (including stock photos & background images)
    - Many images are "decorative" but still convey meaning
    - [Léonie Watson calls these "emotion rich images"](http://tink.uk/text-descriptions-emotion-rich-images/)
  - Only exception is images used as borders, spacers, etc. 
    - meaning of these should be conveyed by the roles on content elements
  
### How?
  - For `<img>` icons, use `alt` to name function
  - For other `<img>`, use `alt` to describe content
    - If complex, use `aria-describedby` to point to longer description on the same page
  - For SVG inline or as `<object>`, use `<title>` and `aria-labelledby`
  - For images embedded using CSS, use `role="img"` and `aria-labelledby`
    - or upgrade to responsive `<img>` with srcset
  - For icon fonts, use [font ligatures](http://thenewcode.com/620/Why-You-Should-Consider-A-Ligature-Icon-Font-For-Your-Next-Project)
    - provides fallback if font doesn't load
    - if not possible, use text in HTML clipped with CSS
  - For localized content, ensure alt text is translated!
  - For user-uploaded images, prompt user to supply alt text
  - If no user text, generate something meaningful with information you have
    - "PNG image uploaded by user AmeliaBR on 19 May 2016"
    - "photo taken on 17 May 2016 in Edmonton, Canada"
  - Don't use `alt=""` for missing description!
  
  


## Communicate the Current State

- Changeable components → States

### Why?

- Often need to know the state of a widget to know what will happen if you use it
- If you're designing different visual states, make sure they are reflected with accessible markup!

### What?

- Any element that can change appearance based on current status
- Form elements with valid/invalid or enabled/disabled states
- On/off switches
- Toggle buttons (e.g., follow/unfollow buttons)
- Tab and accordion headings
- Drag & drop items

### How?

- Complex / custom code will require complex / custom ARIA
- Use native HTML elements whenever possible
  - be careful of checkbox hacks for non-checkboxes!
- Use state attributes for custom toggle-able widgets
  - check-boxes use `aria-checked` (but just use a real checkbox)
  - switches & radio button also use `aria-checked`
  - selection lists use `aria-selected` or `aria-checked`
  - toggle buttons are a button with an `aria-pressed` attribute
  - tabs & accordions use `aria-expanded` on the _clickable_ element
- Use `aria-disabled` and `aria-invalid` for custom form elements
  - `aria-errormessage="message-id"` points to an error that is displayed when `aria-invalid="true"`
- Use [drag and drop attributes](https://www.w3.org/TR/wai-aria-1.1/#attrs_dragdrop) when appropriate
  - also include buttons/forms to make the same changes
  


## Connect Cause and Effect

- Associated components → Relationships

### Why?

- Many users only experience a small part of the page at a time
- When something changes, they need to know what & where
- Relationships implied by colors and layout need to be made explicit

### What?

- Any part of the site where user interaction causes a change elsewhere on the page
  - tabs, accordions, and other expandable text
  - carousels and slide shows
  - tool tips and pop-ups
  - custom audio-video controls
- Any elements which add context to other elements

### How?

- Use `aria-controls="other-element-id"` when an action on this element changes another part of page
  - In some cases, can use HTML `<output>`
- Use `aria-describedby="other-element-id"` when another element provides information to explain this one
  - In addition to `<label>` or `aria-labelledby` for the main label
  - In addition to a good reading order

## Extra credit: Warning about changes

- Anything that is loading or part-way through a change needs `aria-busy="true"`
  - especially important for feeds, etc., where current position could get lost
- Content that might change _without_ user action is "live"
- If changes are important updates, use `aria-live="polite"`
- If changes are urgent alerts, use `aria-live="assertive"`
- If changes don't affect user, use `aria-live="off"`
- Some roles are live regions by default:
  - `alert` for warnings & alerts (assertive by default)
  - `status` and `log` for less urgent updates
  - `marquee` for news headlines and stock tickers--even if they don't scroll! (updates off by default)
  - `timer`
- See also `aria-atomic` and `aria-relevant`



## Styled Text has a Purpose

- Text styles → Semantic HTML

### Why?

- Because it makes your code more readable
- Helps enforce a 1-to-1 relationship between style and meaning
- _May_ be used by some assistive technologies (e.g., Braille)

### What?
- Any content that has a distinct formatting

### How?

- Ask _why_ is this element formatted differently?
- Find an HTML element that matches the meaning
- [There are _a lot_ of HTML elements for text styling!](https://www.w3.org/TR/html51/fullindex.html#index-elements)
  - `<em>` and `<strong>` for emphasis
  - `<dfn>` for a new term being defined
  - `<b>` for other called-out terms or names
  - `<i>` for poetry or foreign language content
  - `<mark>` for highlighted text and pull-quotes
  - `<small>` for fine print
  - `<ins>` and `<del>` for edits
  - `<code>`, `<kbd>`, `<var>`, and `<samp>` for code
  - `<time>` for dates & times (with machine-readable version in `datetime` attribute)
- It's okay to override default formatting for an element
- But respect user expectations
  - links should look like links, other things shouldn't
  - pull quotes are not block quotes
  - color is not enough to distinguish deletions
- These elements are not communicated well by screen readers: make sure text can stand on its own!
  
## Extra credit: Language tags

- Use the `lang` attribute on your root element and again on any content in another language.
- Screen readers need to know what language they're reading!
- Translation services work better if they're not guessing!
- Some CSS (hyphenation, text transform, quotation marks) is language sensitive.
- Some languages affect glyph selection from a font.

<!--
## Extra credit: Machine-readable Markup

- Many semantic HTML elements have special attributes for extra info
- E.g., `datetime` on a `<time>` element
  - `<time datetime="2016-05-19T01:00Z">1AM UTC / 7PM Mountain Time</time>`
- E.g., `cite` on a `<q>` or `<blockquote>` element
  - `<q cite="https://www.w3.org/TR/html51/textlevel-semantics.html#elementdef-q">The use of <code>q</code> elements to mark up quotations is entirely optional</q>`
- Unlike `data-*` attributes, they have standardized syntax & meaning
- Break the cycle of unused HTML features!
-->

## Final Check:<br/> Avoid `<div>` and `<span>`

### Why?
- No meaning without role
- Why would you define styles for content without meaning?

### What?

- Consider this a double-check
- If you've checked everything else, your final code should have very few `<div>` and hardly any `<span>`

### How?
- Use `<div>` (without `role`) only for CSS hacks & JS hooks
  - wrapper for float-based layout
  - placeholder for content that may be injected with script
- Use `<span>` only if no other HTML element suits
  - Or if you need non-meaningful child elements, e.g., fun styles that change on each letter
  


## Good Semantics Don't Fix Bad Design!

- ARIA & HTML semantics help screen readers & some other tools
- HTML semantics also help keyboard users
- Don't help color blindness or many low vision users
  - Still need good color contrast
  - Still need user-friendly font sizes
- Don't help new users, language learners, or people with alternative cognitive processing
  - Still need logical layout with clear flow
  - Still need visible labels for icons & widgets
  - Still need understandable text copy

## Good Semantics ensure <br/>_Everyone_<br/> Appreciates your Good Design


## About Me


- Amelia Bellamy-Royds
  - Author & Web Standards Editor
  - W3C Invited Expert, SVG and ARIA working groups
  - [Books on SVG from O'Reilly Media](http://www.oreilly.com/pub/au/6190)
  - [@AmeliasBrain](https://twitter.com/settings/account)
  - <amelia.bellamy.royds@gmail.com>
  
- Find these slides
  - [AmeliaBR.GitHub.IO/style-is-substance](https://AmeliaBR.GitHub.IO/style-is-substance)