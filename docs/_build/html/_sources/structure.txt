Structure
=========

Document

Doctree element: document.

The top-level element of a parsed reStructuredText document is the "document" element. After initial parsing, the document element is a simple container for a document fragment, consisting of body elements, transitions, and sections, but lacking a document title or other bibliographic elements. The code that calls the parser may choose to run one or more optional post-parse transforms, rearranging the document fragment into a complete document with a title and possibly other metadata elements (author, date, etc.; see Bibliographic Fields).

Specifically, there is no way to indicate a document title and subtitle explicitly in reStructuredText. [1] Instead, a lone top-level section title (see Sections below) can be treated as the document title. Similarly, a lone second-level section title immediately after the "document title" can become the document subtitle. The rest of the sections are then lifted up a level or two. See the DocTitle transform for details.

[1]	The title configuration setting can set a document title that does not become part of the document body.
Sections

Doctree elements: section, title

Sections are identified through their titles, which are marked up with adornment: "underlines" below the title text, or underlines and matching "overlines" above the title. An underline/overline is a single repeated punctuation character that begins in column 1 and forms a line extending at least as far as the right edge of the title text. Specifically, an underline/overline character may be any non-alphanumeric printable 7-bit ASCII character [2]. When an overline is used, the length and character used must match the underline. Underline-only adornment styles are distinct from overline-and-underline styles that use the same character. There may be any number of levels of section titles, although some output formats may have limits (HTML has 6 levels).

[2]	
The following are all valid section title adornment characters:

! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~
Some characters are more suitable than others. The following are recommended:

= - ` : . ' " ~ ^ _ * + #
Rather than imposing a fixed number and order of section title adornment styles, the order enforced will be the order as encountered. The first style encountered will be an outermost title (like HTML H1), the second style will be a subtitle, the third will be a subsubtitle, and so on.

Below are examples of section title styles:


---------------
 Section Title
---------------

When a title has both an underline and an overline, the title text may be inset, as in the first two examples above. This is merely aesthetic and not significant. Underline-only title text may not be inset.

A blank line after a title is optional. All text blocks up to the next title of the same or higher level are included in a section (or subsection, etc.).

All section title styles need not be used, nor need any specific section title style be used. However, a document must be consistent in its use of section titles: once a hierarchy of title styles is established, sections must use that hierarchy.

Each section title automatically generates a hyperlink target pointing to the section. The text of the hyperlink target (the "reference name") is the same as that of the section title. See Implicit Hyperlink Targets for a complete description.

Sections may contain body elements, transitions, and nested sections.

Transitions

Doctree element: transition.

Instead of subheads, extra space or a type ornament between paragraphs may be used to mark text divisions or to signal changes in subject or emphasis.

(The Chicago Manual of Style, 14th edition, section 1.80)

Transitions are commonly seen in novels and short fiction, as a gap spanning one or more lines, with or without a type ornament such as a row of asterisks. Transitions separate other body elements. A transition should not begin or end a section or document, nor should two transitions be immediately adjacent.

The syntax for a transition marker is a horizontal line of 4 or more repeated punctuation characters. The syntax is the same as section title underlines without title text. Transition markers require blank lines before and after:

Para.

----------

Para.
Unlike section title underlines, no hierarchy of transition markers is enforced, nor do differences in transition markers accomplish anything. It is recommended that a single consistent style be used.

The processing system is free to render transitions in output in any way it likes. For example, horizontal rules (<hr>) in HTML output would be an obvious choice.