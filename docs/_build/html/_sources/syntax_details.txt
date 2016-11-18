Syntax Details
=========

Descriptions below list "doctree elements" (document tree element names; XML DTD generic identifiers) corresponding to syntax constructs. For details on the hierarchy of elements, please see The Docutils Document Tree and the Docutils Generic DTD XML document type definition.

Whitespace

Spaces are recommended for indentation, but tabs may also be used. Tabs will be converted to spaces. Tab stops are at every 8th column.

Other whitespace characters (form feeds [chr(12)] and vertical tabs [chr(11)]) are converted to single spaces before processing.

Blank Lines

Blank lines are used to separate paragraphs and other elements. Multiple successive blank lines are equivalent to a single blank line, except within literal blocks (where all whitespace is preserved). Blank lines may be omitted when the markup makes element separation unambiguous, in conjunction with indentation. The first line of a document is treated as if it is preceded by a blank line, and the last line of a document is treated as if it is followed by a blank line.

Indentation

Indentation is used to indicate -- and is only significant in indicating -- block quotes, definitions (in definition list items), and local nested content:


list item content (multi-line contents of list items, and multiple body elements within a list item, including nested lists),
the content of literal blocks, and
the content of explicit markup blocks.
Any text whose indentation is less than that of the current level (i.e., unindented text or "dedents") ends the current level of indentation.

Since all indentation is significant, the level of indentation must be consistent. For example, indentation is the sole markup indicator for block quotes:

This is a top-level paragraph.

    This paragraph belongs to a first-level block quote.

    Paragraph 2 of the first-level block quote.
Multiple levels of indentation within a block quote will result in more complex structures:

This is a top-level paragraph.

    This paragraph belongs to a first-level block quote.

        This paragraph belongs to a second-level block quote.

Another top-level paragraph.

        This paragraph belongs to a second-level block quote.

    This paragraph belongs to a first-level block quote.  The
    second-level block quote above is inside this first-level
    block quote.
When a paragraph or other construct consists of more than one line of text, the lines must be left-aligned:

This is a paragraph.  The lines of
this paragraph are aligned at the left.

    This paragraph has problems.  The
lines are not left-aligned.  In addition
  to potential misinterpretation, warning
    and/or error messages will be generated
  by the parser.
Several constructs begin with a marker, and the body of the construct must be indented relative to the marker. For constructs using simple markers (bullet lists, enumerated lists, footnotes, citations, hyperlink targets, directives, and comments), the level of indentation of the body is determined by the position of the first line of text, which begins on the same line as the marker. For example, bullet list bodies must be indented by at least two columns relative to the left edge of the bullet:

- This is the first line of a bullet list
  item's paragraph.  All lines must align
  relative to the first line.  [1]_

      This indented paragraph is interpreted
      as a block quote.

Because it is not sufficiently indented,
this paragraph does not belong to the list
item.

.. [1] Here's a footnote.  The second line is aligned
   with the beginning of the footnote label.  The ".."
   marker is what determines the indentation.
For constructs using complex markers (field lists and option lists), where the marker may contain arbitrary text, the indentation of the first line after the marker determines the left edge of the body. For example, field lists may have very long markers (containing the field names):

:Hello: This field has a short field name, so aligning the field
        body with the first line is feasible.

:Number-of-African-swallows-required-to-carry-a-coconut: It would
    be very difficult to align the field body with the left edge
    of the first line.  It may even be preferable not to begin the
    body on the same line as the marker.
Escaping Mechanism

The character set universally available to plaintext documents, 7-bit ASCII, is limited. No matter what characters are used for markup, they will already have multiple meanings in written text. Therefore markup characters will sometimes appear in text without being intended as markup. Any serious markup system requires an escaping mechanism to override the default meaning of the characters used for the markup. In reStructuredText we use the backslash, commonly used as an escaping character in other domains.

A backslash followed by any character (except whitespace characters) escapes that character. The escaped character represents the character itself, and is prevented from playing a role in any markup interpretation. The backslash is removed from the output. A literal backslash is represented by two backslashes in a row (the first backslash "escapes" the second, preventing it being interpreted in an "escaping" role).

Backslash-escaped whitespace characters are removed from the document. This allows for character-level inline markup.

There are two contexts in which backslashes have no special meaning: literal blocks and inline literals. In these contexts, a single backslash represents a literal backslash, without having to double up.

Please note that the reStructuredText specification and parser do not address the issue of the representation or extraction of text input (how and in what form the text actually reaches the parser). Backslashes and other characters may serve a character-escaping purpose in certain contexts and must be dealt with appropriately. For example, Python uses backslashes in strings to escape certain characters, but not others. The simplest solution when backslashes appear in Python docstrings is to use raw docstrings:

r"""This is a raw docstring.  Backslashes (\) are not touched."""
Reference Names

Simple reference names are single words consisting of alphanumerics plus isolated (no two adjacent) internal hyphens, underscores, periods, colons and plus signs; no whitespace or other characters are allowed. Footnote labels (Footnotes & Footnote References), citation labels (Citations & Citation References), interpreted text roles, and some hyperlink references use the simple reference name syntax.

Reference names using punctuation or whose names are phrases (two or more space-separated words) are called "phrase-references". Phrase-references are expressed by enclosing the phrase in backquotes and treating the backquoted text as a reference name:

Want to learn about `my favorite programming language`_?

.. _my favorite programming language: http://www.python.org
Simple reference names may also optionally use backquotes.

Reference names are whitespace-neutral and case-insensitive. When resolving reference names internally:

whitespace is normalized (one or more spaces, horizontal or vertical tabs, newlines, carriage returns, or form feeds, are interpreted as a single space), and
case is normalized (all alphabetic characters are converted to lowercase).
For example, the following hyperlink references are equivalent:

- `A HYPERLINK`_
- `a    hyperlink`_
- `A
  Hyperlink`_
Hyperlinks, footnotes, and citations all share the same namespace for reference names. The labels of citations (simple reference names) and manually-numbered footnotes (numbers) are entered into the same database as other hyperlink names. This means that a footnote (defined as ".. [1]") which can be referred to by a footnote reference ([1]_), can also be referred to by a plain hyperlink reference (1). Of course, each type of reference (hyperlink, footnote, citation) may be processed and rendered differently. Some care should be taken to avoid reference name conflicts.