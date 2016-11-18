Body Elements
=============

**Syntax diagram**

+------------------------------+
| paragraph                    |
|                              |
+------------------------------+

+------------------------------+
| paragraSh                    |
|                              |
+------------------------------+


+------------------------------+
| paragraSh                    |
| ASKDASKDJSADJLKJSLKAD        |
+------------------------------+


**Bullet Lists**

- This is the first bullet list item.  The blank line above the
  first list item is required; blank lines between list items
  (such as below this paragraph) are optional.

- This is the first paragraph in the second item in the list.

  This is the second paragraph in the second item in the list.
  The blank line above this paragraph is required.  The left edge
  of this paragraph lines up with the paragraph above, both
  indented relative to the bullet.

  - This is a sublist.  The bullet lines up with the left edge of
    the text blocks above.  A sublist is a new list so requires a
    blank line above and below.

- This is the third item of the main list.

This paragraph is not part of the list.
Here are examples of incorrectly formatted bullet lists:

- This first line is fine.
A blank line is required between list items and paragraphs.
(Warning)

- The following line appears to be a new sublist, but it is not:
  - This is a paragraph continuation, not a sublist (since there's
    no blank line).  This line is also incorrectly indented.
  - Warnings may be issued by the implementation.
Syntax diagram:


**Enumerated Lists**

Examples of nested enumerated lists:

1. Item 1 initial text.

   a) Item 1a.
   b) Item 1b.

2. a) Item 2a.
   b) Item 2b.
Example syntax diagram:


**Definition Lists**

term 1
    Definition 1.

term 2
    Definition 2, paragraph 1.

    Definition 2, paragraph 2.

term 3 : classifier
    Definition 3.

term 4 : classifier one : classifier two
    Definition 4.

**Field Lists**

:Date: 2001-08-16
:Version: 1
:Authors: - Me
          - Myself
          - I
:Indentation: Since the field marker may be quite long, the second
   and subsequent lines of the field body do not have to line up
   with the first line, but they must be indented relative to the
   field name marker, and they must line up with each other.
:Parameter i: integer


**Option Lists**

Doctree elements: option_list, option_list_item, option_group, option, option_string, option_argument, description.

Option lists are two-column lists of command-line options and descriptions, documenting a program's options. For example:

-a         Output all.
-b         Output both (this description is
           quite long).
-c arg     Output just arg.
--long     Output all day long.

-p         This option has two paragraphs in the description.
           This is the first.

           This is the second.  Blank lines may be omitted between
           options (as above) or left in (as here and below).

--very-long-option  A VMS-style option.  Note the adjustment for
                    the required two spaces.

--an-even-longer-option
           The description can also start on the next line.

-2, --two  This option has two variants.

-f FILE, --file=FILE  These two options are synonyms; both have
                      arguments.

/V         A VMS/DOS-style option.


**Literal Blocks**

Doctree element: literal_block.
This is a typical paragraph.  An indented literal block follows.

::

    for a in [5,4,3,2,1]:   # this is program code, shown as-is
        print a
    print "it's..."
    # a literal block continues until the indentation ends


**Expanded form**

Paragraph:

::

    Literal block
Partially minimized form:

Paragraph: ::

    Literal block
Fully minimized form:

Paragraph::

    Literal block


**Indented Literal Blocks**

+------------------------------+
| paragraph                    |
| (ends with "::")             |
+------------------------------+
   +---------------------------+
   | indented literal block    |
   +---------------------------+


**Quoted Literal Blocks**

>> Great idea!
>
> Why didn't I think of that?

You just did!  ;-)
Syntax diagram:

+------------------------------+
| paragraph                    |
| (ends with "::")             |
+------------------------------+
+------------------------------+
| ">" per-line-quoted          |
| ">" contiguous literal block |
+------------------------------+


**Line Blocks**

This example illustrates continuation lines:

| Lend us a couple of bob till Thursday.
| I'm absolutely skint.
| But I'm expecting a postal order and I can pay you back
  as soon as it comes.
| Love, Ewan.
This example illustrates the nesting of line blocks, indicated by the initial indentation of new lines:

Take it away, Eric the Orchestra Leader!

    | A one, two, a one two three four
    |
    | Half a bee, philosophically,
    |     must, *ipso facto*, half not be.
    | But half the bee has got to be,
    |     *vis a vis* its entity.  D'you see?
    |
    | But can a bee be said to be
    |     or not to be an entire bee,
    |         when half the bee is not a bee,
    |             due to some ancient injury?
    |
    | Singing...

Block Quotes

Doctree element: block_quote, attribution.

A text block that is indented relative to the preceding text, without preceding markup indicating it to be a literal block or other content, is a block quote. All markup processing (for body elements and inline markup) continues within the block quote:

This is an ordinary paragraph, introducing a block quote.

    "It is my business to know things.  That is my trade."

    -- Sherlock Holmes
A block quote may end with an attribution: a text block beginning with "--", "---", or a true em-dash, flush left within the block quote. If the attribution consists of multiple lines, the left edges of the second and subsequent lines must align.

Multiple block quotes may occur consecutively if terminated with attributions.

Unindented paragraph.

Block quote 1.

—Attribution 1

Block quote 2.
Empty comments may be used to explicitly terminate preceding constructs that would otherwise consume a block quote:

* List item.

..

    Block quote 3.
Empty comments may also be used to separate block quotes:

    Block quote 4.

..

    Block quote 5.
Blank lines are required before and after a block quote, but these blank lines are not included as part of the block quote.


**Doctest Blocks**

This is an ordinary paragraph.

>>> print 'this is a Doctest block'
this is a Doctest block

The following is a literal block::

    >>> This is not recognized as a doctest block by
    reStructuredText.  It *will* be recognized by the doctest
    module, though!
Indentation is not required for doctest blocks.


**Grid Tables**

+------------------------+------------+----------+----------+
| Header row, column 1   | Header 2   | Header 3 | Header 4 |
| (header rows optional) |            |          |          |
+========================+============+==========+==========+
| body row 1, column 1   | column 2   | column 3 | column 4 |
+------------------------+------------+----------+----------+
| body row 2             | Cells may span columns.          |
+------------------------+------------+---------------------+
| body row 3             | Cells may  | - Table cells       |
+------------------------+ span rows. | - contain           |
| body row 4             |            | - body elements.    |
+------------------------+------------+---------------------+
Some care must be taken with grid tables to avoid undesired interactions with cell text in rare cases. For example, the following table contains a cell in row 2 spanning from column 2 to column 4:

+--------------+----------+-----------+-----------+
| row 1, col 1 | column 2 | column 3  | column 4  |
+--------------+----------+-----------+-----------+
| row 2        |                                  |
+--------------+----------+-----------+-----------+
| row 3        |          |           |           |
+--------------+----------+-----------+-----------+
If a vertical bar is used in the text of that cell, it could have unintended effects if accidentally aligned with column boundaries:

+--------------+----------+-----------+-----------+
| row 1, col 1 | column 2 | column 3  | column 4  |
+--------------+----------+-----------+-----------+
| row 2        | Use the command ``ls | more``.   |
+--------------+----------+-----------+-----------+
| row 3        |          |           |           |
+--------------+----------+-----------+-----------+
Several solutions are possible. All that is needed is to break the continuity of the cell outline rectangle. One possibility is to shift the text by adding an extra space before:

+--------------+----------+-----------+-----------+
| row 1, col 1 | column 2 | column 3  | column 4  |
+--------------+----------+-----------+-----------+
| row 2        |  Use the command ``ls | more``.  |
+--------------+----------+-----------+-----------+
| row 3        |          |           |           |
+--------------+----------+-----------+-----------+
Another possibility is to add an extra line to row 2:

+--------------+----------+-----------+-----------+
| row 1, col 1 | column 2 | column 3  | column 4  |
+--------------+----------+-----------+-----------+
| row 2        | Use the command ``ls | more``.   |
|              |                                  |
+--------------+----------+-----------+-----------+
| row 3        |          |           |           |
+--------------+----------+-----------+-----------+


**Simple Tables**

=====  =====  =======
  A      B    A and B
=====  =====  =======
False  False  False
True   False  False
False  True   False
True   True   True
=====  =====  =======

=====  =====  ======
   Inputs     Output
------------  ------
  A      B    A or B
=====  =====  ======
False  False  False
True   False  True
False  True   True
True   True   True
=====  =====  ======

=====  =====
col 1  col 2
=====  =====
1      Second column of row 1.
2      Second column of row 2.
       Second line of paragraph.
3      - Second column of row 3.

       - Second item in bullet
         list (row 3, column 2).
\      Row 4; column 1 will be empty.
=====  =====


**Explicit Markup Blocks**


.. [1] Body elements go here.



**Auto-Numbered Footnotes**

[#note]_ 
[#note]_


([#]_)


.. [#] This is footnote 1.
.. [#] This is footnote 2.
.. [#] This is footnote 3.

