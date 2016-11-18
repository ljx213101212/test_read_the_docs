Body Elements 2
===============

Auto-Symbol Footnotes

An asterisk ("*") may be used for footnote labels to request automatic symbol generation for footnotes and footnote references. The asterisk may be the only character in the label. For example:

Here is a symbolic footnote reference: [*]_.

.. [*] This is the footnote.


Note



[2]_ will be "2" (manually numbered),
[#]_ will be "3" (anonymous auto-numbered), and
[#label]_ will be "1" (labeled auto-numbered).

.. [2] This footnote is labeled manually, so its number is fixed.

.. [#label] This autonumber-labeled footnote will be labeled "1".
   It is the first auto-numbered footnote and no other footnote
   with label "1" exists.  The order of the footnotes is used to
   determine numbering, not the order of the footnote references.

.. [#] This footnote will be labeled "3".  It is the second
   auto-numbered footnote, but footnote label "2" is already used.
Citations

See also: Citation References.

Doctree element: citation

Citations are identical to footnotes except that they use only non-numeric labels such as [note] or [GVR2001]. Citation labels are simple reference names (case-insensitive single words consisting of alphanumerics plus internal hyphens, underscores, and periods; no whitespace). Citations may be rendered separately and differently from footnotes. For example:

Here is a citation reference: [CIT2002]_.

.. [CIT2002] This is the citation.  It's just like a footnote,
   except the label is textual.
Hyperlink Targets

Clicking on this internal hyperlink will take us to the target_
below.

.. _target:

.. _target1:
.. _target2:



.. _Python DOC-SIG mailing list archive:
.. _archive:
.. _Doc-SIG: http://mail.python.org/pipermail/doc-sig/


**Directives**

Doctree elements: depend on the directive.

Directives are an extension mechanism for reStructuredText, a way of adding support for new constructs without adding new primary syntax (directives may support additional syntax locally). All standard directives (those implemented and registered in the reference reStructuredText parser) are described in the reStructuredText Directives document, and are always available. Any other directives are domain-specific, and may require special action to make them available when processing the document.

For example, here's how an image may be placed:

.. image:: dhi_logo_pos_rgb.png
A figure (a graphic with a caption) may placed like this:

.. figure:: larch.png

   The larch.
An admonition (note, caution, etc.) contains other body elements:


.. note:: HAHAHA


.. note:: This is a paragraph

   - Here is a bullet list.
Directives are indicated by an explicit markup start (".. ") followed by the directive type, two colons, and whitespace (together called the "directive marker"). Directive types are case-insensitive single words (alphanumerics plus isolated internal hyphens, underscores, plus signs, colons, and periods; no whitespace). Two colons are used after the directive type for these reasons:

Two colons are distinctive, and unlikely to be used in common text.

Two colons avoids clashes with common comment text like:

.. Danger: modify at your own risk!
If an implementation of reStructuredText does not recognize a directive (i.e., the directive-handler is not installed), a level-3 (error) system message is generated, and the entire directive block (including the directive itself) will be included as a literal block. Thus "::" is a natural choice.

The directive block is consists of any text on the first line of the directive after the directive marker, and any subsequent indented text. The interpretation of the directive block is up to the directive code. There are three logical parts to the directive block:

Directive arguments.
Directive options.
Directive content.
Individual directives can employ any combination of these parts. Directive arguments can be filesystem paths, URLs, title text, etc. Directive options are indicated using field lists; the field names and contents are directive-specific. Arguments and options must form a contiguous block beginning on the first or second line of the directive; a blank line indicates the beginning of the directive content block. If either arguments and/or options are employed by the directive, a blank line must separate them from the directive content. The "figure" directive employs all three parts:

.. figure:: larch.png
   :scale: 50

   The larch.
Simple directives may not require any content. If a directive that does not employ a content block is followed by indented text anyway, it is an error. If a block quote should immediately follow a directive, use an empty comment in-between (see Comments below).

Actions taken in response to directives and the interpretation of text in the directive content block or subsequent text block(s) are directive-dependent. See reStructuredText Directives for details.

Directives are meant for the arbitrary processing of their contents, which can be transformed into something possibly unrelated to the original text. It may also be possible for directives to be used as pragmas, to modify the behavior of the parser, such as to experiment with alternate syntax. There is no parser support for this functionality at present; if a reasonable need for pragma directives is found, they may be supported.

Directives do not generate "directive" elements; they are a parser construct only, and have no intrinsic meaning outside of reStructuredText. Instead, the parser will transform recognized directives into (possibly specialized) document elements. Unknown directives will trigger level-3 (error) system messages.

Syntax diagram:

+-------+-------------------------------+
| ".. " | directive type "::" directive |
+-------+ block                         |
        |                               |
        +-------------------------------+
Substitution Definitions

Doctree element: substitution_definition.

Substitution definitions are indicated by an explicit markup start (".. ") followed by a vertical bar, the substitution text, another vertical bar, whitespace, and the definition block. Substitution text may not begin or end with whitespace. A substitution definition block contains an embedded inline-compatible directive (without the leading ".. "), such as "image" or "replace". For example:

The |biohazard| symbol must be used on containers used to
dispose of medical waste.

.. |biohazard| image:: biohazard.png
It is an error for a substitution definition block to directly or indirectly contain a circular substitution reference.

Substitution references are replaced in-line by the processed contents of the corresponding definition (linked by matching substitution text). Matches are case-sensitive but forgiving; if no exact match is found, a case-insensitive comparison is attempted.

Substitution definitions allow the power and flexibility of block-level directives to be shared by inline text. They are a way to include arbitrarily complex inline structures within text, while keeping the details out of the flow of text. They are the equivalent of SGML/XML's named entities or programming language macros.

Without the substitution mechanism, every time someone wants an application-specific new inline structure, they would have to petition for a syntax change. In combination with existing directive syntax, any inline structure can be coded without new syntax (except possibly a new directive).

Syntax diagram:

+-------+-----------------------------------------------------+
| ".. " | "|" substitution text "| " directive type "::" data |
+-------+ directive block                                     |
        |                                                     |
        +-----------------------------------------------------+
Following are some use cases for the substitution mechanism. Please note that most of the embedded directives shown are examples only and have not been implemented.

Objects
Substitution references may be used to associate ambiguous text with a unique object identifier.

For example, many sites may wish to implement an inline "user" directive:

|Michael| and |Jon| are our widget-wranglers.

.. |Michael| user:: mjones
.. |Jon|     user:: jhl
Depending on the needs of the site, this may be used to index the document for later searching, to hyperlink the inline text in various ways (mailto, homepage, mouseover Javascript with profile and contact information, etc.), or to customize presentation of the text (include username in the inline text, include an icon image with a link next to the text, make the text bold or a different color, etc.).

The same approach can be used in documents which frequently refer to a particular type of objects with unique identifiers but ambiguous common names. Movies, albums, books, photos, court cases, and laws are possible. For example:

|The Transparent Society| offers a fascinating alternate view
on privacy issues.

.. |The Transparent Society| book:: isbn=0738201448
Classes or functions, in contexts where the module or class names are unclear and/or interpreted text cannot be used, are another possibility:

4XSLT has the convenience method |runString|, so you don't
have to mess with DOM objects if all you want is the
transformed output.

.. |runString| function:: module=xml.xslt class=Processor
Images
Images are a common use for substitution references:

West led the |H| 3, covered by dummy's |H| Q, East's |H| K,
and trumped in hand with the |S| 2.

.. |H| image:: /images/heart.png
   :height: 11
   :width: 11
.. |S| image:: /images/spade.png
   :height: 11
   :width: 11

* |Red light| means stop.
* |Green light| means go.
* |Yellow light| means go really fast.

.. |Red light|    image:: red_light.png
.. |Green light|  image:: green_light.png
.. |Yellow light| image:: yellow_light.png

|-><-| is the official symbol of POEE_.

.. |-><-| image:: discord.png
.. _POEE: http://www.poee.org/
The "image" directive has been implemented.
Styles [9]
Substitution references may be used to associate inline text with an externally defined presentation style:

Even |the text in Texas| is big.

.. |the text in Texas| style:: big
The style name may be meaningful in the context of some particular output format (CSS class name for HTML output, LaTeX style name for LaTeX, etc), or may be ignored for other output formats (such as plaintext).

[9] There may be sufficient need for a "style" mechanism to warrant simpler syntax such as an extension to the interpreted text role syntax. The substitution mechanism is cumbersome for simple text styling.
Templates
Inline markup may be used for later processing by a template engine. For example, a Zope author might write:

Welcome back, |name|!

.. |name| tal:: replace user/getUserName
After processing, this ZPT output would result:

Welcome back,
<span tal:replace="user/getUserName">name</span>!
Zope would then transform this to something like "Welcome back, David!" during a session with an actual user.
Replacement text
The substitution mechanism may be used for simple macro substitution. This may be appropriate when the replacement text is repeated many times throughout one or more documents, especially if it may need to change later. A short example is unavoidably contrived:

|RST|_ is a little annoying to type over and over, especially
when writing about |RST| itself, and spelling out the
bicapitalized word |RST| every time isn't really necessary for
|RST| source readability.

.. |RST| replace:: reStructuredText
.. _RST: http://docutils.sourceforge.net/rst.html
Note the trailing underscore in the first use of a substitution reference. This indicates a reference to the corresponding hyperlink target.

Substitution is also appropriate when the replacement text cannot be represented using other inline constructs, or is obtrusively long:

But still, that's nothing compared to a name like
|j2ee-cas|__.

.. |j2ee-cas| replace::
   the Java `TM`:super: 2 Platform, Enterprise Edition Client
   Access Services
__ http://developer.java.sun.com/developer/earlyAccess/
   j2eecas/
The "replace" directive has been implemented.
Comments

Doctree element: comment.

Arbitrary indented text may follow the explicit markup start and will be processed as a comment element. No further processing is done on the comment block text; a comment contains a single "text blob". Depending on the output formatter, comments may be removed from the processed output. The only restriction on comments is that they not use the same syntax as any of the other explicit markup constructs: substitution definitions, directives, footnotes, citations, or hyperlink targets. To ensure that none of the other explicit markup constructs is recognized, leave the ".." on a line by itself:

.. This is a comment
..
   _so: is this!
..
   [and] this!
..
   this:: too!
..
   |even| this:: !
An explicit markup start followed by a blank line and nothing else (apart from whitespace) is an "empty comment". It serves to terminate a preceding construct, and does not consume any indented text following. To have a block quote follow a list or any indented construct, insert an unindented empty comment in-between.

Syntax diagram:

+-------+----------------------+
| ".. " | comment              |
+-------+ block                |
        |                      |
        +----------------------+
Implicit Hyperlink Targets

Implicit hyperlink targets are generated by section titles, footnotes, and citations, and may also be generated by extension constructs. Implicit hyperlink targets otherwise behave identically to explicit hyperlink targets.

Problems of ambiguity due to conflicting duplicate implicit and explicit reference names are avoided by following this procedure:

Explicit hyperlink targets override any implicit targets having the same reference name. The implicit hyperlink targets are removed, and level-1 (info) system messages are inserted.
Duplicate implicit hyperlink targets are removed, and level-1 (info) system messages inserted. For example, if two or more sections have the same title (such as "Introduction" subsections of a rigidly-structured document), there will be duplicate implicit hyperlink targets.
Duplicate explicit hyperlink targets are removed, and level-2 (warning) system messages are inserted. Exception: duplicate external hyperlink targets (identical hyperlink names and referenced URIs) do not conflict, and are not removed.
System messages are inserted where target links have been removed. See "Error Handling" in PEP 258.

The parser must return a set of unique hyperlink targets. The calling software (such as the Docutils) can warn of unresolvable links, giving reasons for the messages.

Inline Markup

In reStructuredText, inline markup applies to words or phrases within a text block. The same whitespace and punctuation that serves to delimit words in written text is used to delimit the inline markup syntax constructs (see the inline markup recognition rules for details). The text within inline markup may not begin or end with whitespace. Arbitrary character-level inline markup is supported although not encouraged. Inline markup cannot be nested.

There are nine inline markup constructs. Five of the constructs use identical start-strings and end-strings to indicate the markup:

emphasis: "*"
strong emphasis: "**"
interpreted text: "`"
inline literals: "``"
substitution references: "|"
Three constructs use different start-strings and end-strings:

inline internal targets: "_`" and "`"
footnote references: "[" and "]_"
hyperlink references: "`" and "`_" (phrases), or just a trailing "_" (single words)
Standalone hyperlinks are recognized implicitly, and use no extra markup.

Inline markup recognition rules

Inline markup start-strings and end-strings are only recognized if the following conditions are met:

Inline markup start-strings must be immediately followed by non-whitespace.
Inline markup end-strings must be immediately preceded by non-whitespace.
The inline markup end-string must be separated by at least one character from the start-string.
Both, inline markup start-string and end-string must not be preceded by an unescaped backslash (except for the end-string of inline literals). See Escaping Mechanism above for details.
If an inline markup start-string is immediately preceded by one of the ASCII characters ' " < ( [ { or a similar Unicode character[10], it must not be followed by the corresponding closing character from ' " ) ] } > or a similar Unicode character[11]. (For quotes, corresponding characters can be any of the quotation marks in international usage.)
If the configuration setting simple-inline-markup is False (default), additional conditions apply to the characters "around" the inline markup:

Inline markup start-strings must start a text block or be immediately preceded by
whitespace,
one of the ASCII characters - : / ' " < ( [ {
or a similar Unicode punctuation character.[12]
Inline markup end-strings must end a text block or be immediately followed by
whitespace,
one of the ASCII characters - . , : ; ! ? \ / ' " ) ] } >
or a similar Unicode punctuation character.[13]
[10]  Unicode categories Ps, Pi, or Pf
[11]  Unicode categories Pe, Pf, or Pi
[12]  Unicode categories Pd (Dash), Po (Other), Pi (Initial quote), Pf (Final quote), or Ps (Open)
[13]  Unicode categories Pd (Dash), Po (Other), Pi (Initial quote), Pf (Final quote), or Pe (Close)
The inline markup recognition rules were devised to allow 90% of non-markup uses of "*", "`", "_", and "|" without escaping. For example, none of the following terms are recognized as containing inline markup strings:

2 * x a ** b (* BOM32_* ` `` _ __ | (breaks 1)
|| (breaks 3)
"*" '|' (*) [*] {*} <*> ‘*’ ‚*‘ ‘*‚ ’*’ ‚*’ “*” „*“ “*„ ”*” „*” »*« ›*‹ «*» »*» ›*› (breaks 5)
2*x a**b O(N**2) e**(x*y) f(x)*f(y) a|b file*.* __init__ __init__() (breaks 6)
No escaping is required inside the following inline markup examples:

2 * x *a **b *.txt (breaks 2)
2*x a**b O(N**2) e**(x*y) f(x)*f(y) a*(1+2) (breaks 7)
It may be desirable to use inline literals for some of these anyhow, especially if they represent code snippets. It's a judgment call.

These cases do require either literal-quoting or escaping to avoid misinterpretation:

*4, class_, *args, **kwargs, `TeX-quoted', *ML, *.txt
In most use cases, inline literals or literal blocks are the best choice (by default, this also selects a monospaced font):

*4, class_, *args, **kwargs, `TeX-quoted', *ML, *.txt
For languages that don't use whitespace between words (e.g. Japanese or Chinese) it is recommended to set simple-inline-markup to True and eventually escape inline markup characters. The examples breaking rules 6 and 7 above show which constructs may need special attention.

Recognition order

Inline markup delimiter characters are used for multiple constructs, so to avoid ambiguity there must be a specific recognition order for each character. The inline markup recognition order is as follows:

Asterisks: Strong emphasis ("**") is recognized before emphasis ("*").
Backquotes: Inline literals ("``"), inline internal targets (leading "_`", trailing "`"), are mutually independent, and are recognized before phrase hyperlink references (leading "`", trailing "`_") and interpreted text ("`").
Trailing underscores: Footnote references ("[" + label + "]_") and simple hyperlink references (name + trailing "_") are mutually independent.
Vertical bars: Substitution references ("|") are independently recognized.
Standalone hyperlinks are the last to be recognized.
Character-Level Inline Markup

It is possible to mark up individual characters within a word with backslash escapes (see Escaping Mechanism above). Backslash escapes can be used to allow arbitrary text to immediately follow inline markup:

Python ``list``\s use square bracket syntax.
The backslash will disappear from the processed document. The word "list" will appear as inline literal text, and the letter "s" will immediately follow it as normal text, with no space in-between.

Arbitrary text may immediately precede inline markup using backslash-escaped whitespace:

Possible in *re*\ ``Structured``\ *Text*, though not encouraged.
The backslashes and spaces separating "re", "Structured", and "Text" above will disappear from the processed document.

Caution!

The use of backslash-escapes for character-level inline markup is not encouraged. Such use is ugly and detrimental to the unprocessed document's readability. Please use this feature sparingly and only where absolutely necessary.
Emphasis

Doctree element: emphasis.

Start-string = end-string = "*".

Text enclosed by single asterisk characters is emphasized:

This is *emphasized text*.
Emphasized text is typically displayed in italics.

Strong Emphasis

Doctree element: strong.

Start-string = end-string = "**".

Text enclosed by double-asterisks is emphasized strongly:

This is **strong text**.
Strongly emphasized text is typically displayed in boldface.

Interpreted Text

Doctree element: depends on the explicit or implicit role and processing.

Start-string = end-string = "`".

Interpreted text is text that is meant to be related, indexed, linked, summarized, or otherwise processed, but the text itself is typically left alone. Interpreted text is enclosed by single backquote characters:

This is `interpreted text`.
The "role" of the interpreted text determines how the text is interpreted. The role may be inferred implicitly (as above; the "default role" is used) or indicated explicitly, using a role marker. A role marker consists of a colon, the role name, and another colon. A role name is a single word consisting of alphanumerics plus isolated internal hyphens, underscores, plus signs, colons, and periods; no whitespace or other characters are allowed. A role marker is either a prefix or a suffix to the interpreted text, whichever reads better; it's up to the author:

:role:`interpreted text`

`interpreted text`:role:
Interpreted text allows extensions to the available inline descriptive markup constructs. To emphasis, strong emphasis, inline literals, and hyperlink references, we can add "title reference", "index entry", "acronym", "class", "red", "blinking" or anything else we want. Only pre-determined roles are recognized; unknown roles will generate errors. A core set of standard roles is implemented in the reference parser; see reStructuredText Interpreted Text Roles for individual descriptions. The role directive can be used to define custom interpreted text roles. In addition, applications may support specialized roles.

Inline Literals

Doctree element: literal.

Start-string = end-string = "``".

Text enclosed by double-backquotes is treated as inline literals:

This text is an example of ``inline literals``.
Inline literals may contain any characters except two adjacent backquotes in an end-string context (according to the recognition rules above). No markup interpretation (including backslash-escape interpretation) is done within inline literals.

Line breaks are not preserved in inline literals. Although a reStructuredText parser will preserve runs of spaces in its output, the final representation of the processed document is dependent on the output formatter, thus the preservation of whitespace cannot be guaranteed. If the preservation of line breaks and/or other whitespace is important, literal blocks should be used.

Inline literals are useful for short code snippets. For example:

The regular expression ``[+-]?(\d+(\.\d*)?|\.\d+)`` matches
floating-point numbers (without exponents).
Hyperlink References

Doctree element: reference.

Named hyperlink references:
Start-string = "" (empty string), end-string = "_".
Start-string = "`", end-string = "`_". (Phrase references.)
Anonymous hyperlink references:
Start-string = "" (empty string), end-string = "__".
Start-string = "`", end-string = "`__". (Phrase references.)
Hyperlink references are indicated by a trailing underscore, "_", except for standalone hyperlinks which are recognized independently. The underscore can be thought of as a right-pointing arrow. The trailing underscores point away from hyperlink references, and the leading underscores point toward hyperlink targets.

Hyperlinks consist of two parts. In the text body, there is a source link, a reference name with a trailing underscore (or two underscores for anonymous hyperlinks):

See the Python_ home page for info.
A target link with a matching reference name must exist somewhere else in the document. See Hyperlink Targets for a full description).

Anonymous hyperlinks (which see) do not use reference names to match references to targets, but otherwise behave similarly to named hyperlinks.

Embedded URIs and Aliases

A hyperlink reference may directly embed a target URI or (since Docutils 0.11) a hyperlink reference within angle brackets ("<...>") as follows:

See the `Python home page <http://www.python.org>`_ for info.

This `link <Python home page_>`_ is an alias to the link above.
This is exactly equivalent to:

See the `Python home page`_ for info.

This link_ is an alias to the link above.

.. _Python home page: http://www.python.org
.. _link: `Python home page`_
The bracketed URI must be preceded by whitespace and be the last text before the end string.

With a single trailing underscore, the reference is named and the same target URI may be referred to again. With two trailing underscores, the reference and target are both anonymous, and the target cannot be referred to again. These are "one-off" hyperlinks. For example:

`RFC 2396 <http://www.rfc-editor.org/rfc/rfc2396.txt>`__ and `RFC
2732 <http://www.rfc-editor.org/rfc/rfc2732.txt>`__ together
define the syntax of URIs.
Equivalent to:

`RFC 2396`__ and `RFC 2732`__ together define the syntax of URIs.

__ http://www.rfc-editor.org/rfc/rfc2396.txt
__ http://www.rfc-editor.org/rfc/rfc2732.txt
Standalone hyperlinks are treated as URIs, even if they end with an underscore like in the example of a Python function documentation:

`__init__ <http:example.py.html#__init__>`__
If a target URI that is not recognized as standalone hyperlink happens to end with an underscore, this needs to be backslash-escaped to avoid being parsed as hyperlink reference. For example

Use the `source <parrots.txt\_>`__.
creates an anonymous reference to the file parrots.txt_.

If the reference text happens to end with angle-bracketed text that is not a URI or hyperlink reference, at least one angle-bracket needs to be backslash-escaped or an escaped space should follow. For example, here are three references to titles describing a tag:

See `HTML Element: \<a>`_, `HTML Element: <b\> `_, and
`HTML Element: <c>\ `_.
The reference text may also be omitted, in which case the URI will be duplicated for use as the reference text. This is useful for relative URIs where the address or file name is also the desired reference text:

See `<a_named_relative_link>`_ or `<an_anonymous_relative_link>`__
for details.
Caution!

This construct offers easy authoring and maintenance of hyperlinks at the expense of general readability. Inline URIs, especially long ones, inevitably interrupt the natural flow of text. For documents meant to be read in source form, the use of independent block-level hyperlink targets is strongly recommended. The embedded URI construct is most suited to documents intended only to be read in processed form.
Inline Internal Targets

Doctree element: target.

Start-string = "_`", end-string = "`".

Inline internal targets are the equivalent of explicit internal hyperlink targets, but may appear within running text. The syntax begins with an underscore and a backquote, is followed by a hyperlink name or phrase, and ends with a backquote. Inline internal targets may not be anonymous.

For example, the following paragraph contains a hyperlink target named "Norwegian Blue":

Oh yes, the _`Norwegian Blue`.  What's, um, what's wrong with it?
See Implicit Hyperlink Targets for the resolution of duplicate reference names.

Footnote References

See also: Footnotes

Doctree element: footnote_reference.

Configuration settings: footnote_references, trim_footnote_reference_space.

Start-string = "[", end-string = "]_".

Each footnote reference consists of a square-bracketed label followed by a trailing underscore. Footnote labels are one of:

one or more digits (i.e., a number),
a single "#" (denoting auto-numbered footnotes),
a "#" followed by a simple reference name (an autonumber label), or
a single "*" (denoting auto-symbol footnotes).
For example:

Please RTFM [1]_.

.. [1] Read The Fine Manual
Inline markup recognition rules may require whitespace in front of the footnote reference. To remove the whitespace from the output, use an escaped whitespace character (see Escaping Mechanism) or set the trim_footnote_reference_space configuration setting. Leading whitespace is removed by default, if the footnote_references setting is "superscript".

Citation References

See also: Citations

Doctree element: citation_reference.

Start-string = "[", end-string = "]_".

Each citation reference consists of a square-bracketed label followed by a trailing underscore. Citation labels are simple reference names (case-insensitive single words, consisting of alphanumerics plus internal hyphens, underscores, and periods; no whitespace).

For example:

Here is a citation reference: [CIT2002]_.
Substitution References

Doctree element: substitution_reference, reference.

Start-string = "|", end-string = "|" (optionally followed by "_" or "__").

Vertical bars are used to bracket the substitution reference text. A substitution reference may also be a hyperlink reference by appending a "_" (named) or "__" (anonymous) suffix; the substitution text is used for the reference text in the named case.

The processing system replaces substitution references with the processed contents of the corresponding substitution definitions (which see for the definition of "correspond"). Substitution definitions produce inline-compatible elements.

Examples:

This is a simple |substitution reference|.  It will be replaced by
the processing system.

This is a combination |substitution and hyperlink reference|_.  In
addition to being replaced, the replacement text or element will
refer to the "substitution and hyperlink reference" target.
Standalone Hyperlinks

Doctree element: reference.

Start-string = end-string = "" (empty string).

A URI (absolute URI [14] or standalone email address) within a text block is treated as a general external hyperlink with the URI itself as the link's text. For example:

See http://www.python.org for info.
would be marked up in HTML as:

See <a href="http://www.python.org">http://www.python.org</a> for
info.
Two forms of URI are recognized:

Absolute URIs. These consist of a scheme, a colon (":"), and a scheme-specific part whose interpretation depends on the scheme.

The scheme is the name of the protocol, such as "http", "ftp", "mailto", or "telnet". The scheme consists of an initial letter, followed by letters, numbers, and/or "+", "-", ".". Recognition is limited to known schemes, per the Official IANA Registry of URI Schemes and the W3C's Retired Index of WWW Addressing Schemes.

The scheme-specific part of the resource identifier may be either hierarchical or opaque:

Hierarchical identifiers begin with one or two slashes and may use slashes to separate hierarchical components of the path. Examples are web pages and FTP sites:

http://www.python.org

ftp://ftp.python.org/pub/python
Opaque identifiers do not begin with slashes. Examples are email addresses and newsgroups:

mailto:someone@somewhere.com

news:comp.lang.python
With queries, fragments, and %-escape sequences, URIs can become quite complicated. A reStructuredText parser must be able to recognize any absolute URI, as defined in RFC2396 and RFC2732.

Standalone email addresses, which are treated as if they were absolute URIs with a "mailto:" scheme. Example:

someone@somewhere.com
Punctuation at the end of a URI is not considered part of the URI, unless the URI is terminated by a closing angle bracket (">"). Backslashes may be used in URIs to escape markup characters, specifically asterisks ("*") and underscores ("_") which are vaid URI characters (see Escaping Mechanism above).

[14]  Uniform Resource Identifier. URIs are a general form of URLs (Uniform Resource Locators). For the syntax of URIs see RFC2396 and RFC2732.
Units

(New in Docutils 0.3.10.)

All measures consist of a positive floating point number in standard (non-scientific) notation and a unit, possibly separated by one or more spaces.

Units are only supported where explicitly mentioned in the reference manuals.

Length Units

The following length units are supported by the reStructuredText parser:

em (ems, the height of the element's font)
ex (x-height, the height of the letter "x")
px (pixels, relative to the canvas resolution)
in (inches; 1in=2.54cm)
cm (centimeters; 1cm=10mm)
mm (millimeters)
pt (points; 1pt=1/72in)
pc (picas; 1pc=12pt)
This set corresponds to the length units in CSS.

(List and explanations taken from http://www.htmlhelp.com/reference/css/units.html#length.)

The following are all valid length values: "1.5em", "20 mm", ".5in".

Length values without unit are completed with a writer-dependent default (e.g. px with html4css1, pt with latex2e). See the writer specific documentation in the user doc for details.

Percentage Units

Percentage values have a percent sign ("%") as unit. Percentage values are relative to other values, depending on the context in which they occur.
