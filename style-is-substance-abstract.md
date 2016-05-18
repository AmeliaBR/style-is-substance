Style Is Substance
==================

Outline for a talk by
Amelia Bellamy-Royds
as part of the Inclusive Design 24 virtual conference, 19 May 2016


Short version:
--------------

Visual style is often described in contrast to the document semantics defined by HTML tags and ARIA roles.
But in a well-designed website or document, 
style provides the semantic information to visual users.
It conveys structure, function, and relationships.
Visual designers understand these semantics implicitly, 
but that knowledge is often not translated into the markup.
As a result, those semantics are not available to non-visual or modified-visual users.
I will demonstrate how the common motifs of visual web design can be translated into accessible markup,
by working through some standard web designs, parsing the visual styles into landmarks and headings.




Long version:
-------------

Visual style in a well-designed website or document is not decoration.
Instead, it is an important layer of non-verbal communication.
The layout, the colors, the fonts and font sizes, the images and the animation:
they communicate branding and style, 
but also the fundamental structure and purpose of each component and the relationships between them.

These aspecs are collectively known as the structural semantics of the document.
Semantics are key to making web documents accessible.
They allow the fundamental meaning to be preserved in alternative presentations.
In HTML and SVG, structure and purpose of each part must be marked up using tags or attributes that the browser can recognize and translate for assistive technologies.
That way, users who cannot appreciate the meaning conveyed by the visual cues can perceive it through alternate hints, such as high-contrast colors or spoken descriptions, 
and users can interact with the document using alternate input methods.

Markup semantics are often contrasted against visual style.  “Use semantic content, not styles, to convey meaning,” is common advice.
This assumes an idealized workflow that starts with fully marked-up HTML, adding visual styles later.
But the reality is that most designers start with visual mock-ups, 
and only translate it to code after the structure of the visual document has been determined.  

By belittling the importance of visual semantics,
accessibility advocates alienate potential allies in the web development team.
Visual designers specialize in semantics, even if they don't use that word.
Nearly any feature that is important to a visual design is important for accessibility semantics.

What is needed — beyond increased mutual respect — is a common language,
a process for translating the visual designer's language into HTML tags and ARIA roles.
I will demonstrate the first steps of that process by working through some standard web designs,
showing how the visual styles can be parsed into the semantic language of landmarks and headings.

That means:

- Identifying the main content in a web page

- Categorizing the rest of the content into appropriate landmark types: headers, footers, navigation, sidebars, and knowing both the HTML and ARIA terms for them (they're not the same!)

- Creating a useful outline of headings, sections, or articles dividing up large blocks of content

- Understanding text-level semantics that distinguish spans and blocks of text

Text level semantics are usually easy to parse in a standard blog post or news article, 
since the language we use to describe the content matches the language used in HTML and ARIA.  
But app-like web designs and graphics have analagous structures, and these should be leveraged whenever possible.
In each case, the question is: 
what does the visual formatting mean, and how can the same meaning be conveyed in markup?

<!--

Some further steps to the process, for which there won't be time in a 45min talk.  Left here for reference in case of a sequel:

- Capturing the relevance of an image or complex graphic in alternative text

- Associating explanatory content, tips, and warnings with the text or widget it describes

- Distinguishing between links, buttons, and forms so that their behavior matches the expectations of all users

- Ensuring changes to the web page are logically presented, with clear cause and effect

-->