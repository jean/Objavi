================================================
Objavi2: another FLOSS Manuals publishing system
================================================

Introduction
============

FLOSS Manuals books are written and stored as HTML, but are usually
converted to PDF, epub, or ODF for distribution or printing.  Programs
which perform this task are called objavi (pronounced "ob-Yah-vee"),
after the Croatian word "objavi!" meaning "publish!".

The previous objavi, Objavi beta, could produce very good PDF
documents using Latin text, but did not cope well with other scripts,
and could not produce other output.  Objavi 2 was originally written
just to provide fully internationalised PDFs, but it has since been
adapted to produce other formats.

Objavi 2 is free software, distributed under the version 3 or greater
of the GNU Affero General Public License.  The source can be viewed at

 http://booki-dev.flossmanuals.net/git?p=objavi2.git
 (or, alternatively, http://repo.or.cz/w/objavi2.git)

which also contains instructions for cloning the git repository.  If
you want a source tarball without worrying about git, try this link:

 http://repo.or.cz/w/objavi2.git?a=snapshot;h=HEAD;sf=tgz

It is primarily written in Python, with a substantial amount of
QSAScript (an ECMAscript variant) and some Javascript, HTML, and CSS.

The development of Objavi2 was supported by Internews.  It was
extended to produce epub documents with support from the Internet
Archive.


The objavi process
==================

Objavi2 starts with a "booki-zip", as defined in the file
"booki-zip-standard/txt".  This might be sourced from a Booki
instance, or from Twiki via the booki-twiki-gateway script, or perhaps
form an epub imported via Espri.

PDF Output
~~~~~~~~~~
If a PDF is required, the HTML is concatenated, various extra bits are
inserted, and the wkhtmltopdf program rederes it using WebKit.

At this point the PDF has no page numbers, no gutters, no table of
contents, and is using a too big paper size.  In order to write a
table of contents, an outline of the PDF is extracted and laid out as
html.  The table of contents thus generated is combined with other
preliminary pages and another PDF is created.

If a book PDF is required, Pdfedit is used to crop the pages down to
size and to shift them alternately left and right, creating a gutter
for the spine of the book.  Then pdfedit is used again to add page
numbers to both PDFs, with lowercase roman numbers being used for the
preliminary pages.

Finally the two PDFs are combined using pdftk and, optionally, spun
180 degrees so they appear upside down.  If a right-to-left book is
printed like this on a left-to-right printer, the binding will be on
the correct side.

Pdfedit and wkhtmltopdf both require an X server to run, for which
Xvfb is used.

For newspaper format, the page size is set to the column width, and
pdfnup is used to arrange the columns on another page.

OpenOffice output
~~~~~~~~~~~~~~~~~
ODF output was introduced with Objavi 2.1.  This uses an Open Office
instance controlled by pyuno.

Epub output
~~~~~~~~~~~
The html in the booki-zip is manipulated into xhtml using lxml, and
the structural information and metadata is converted into epub form.


Future plans
============

See http://booki-dev.flossmanuals.net/report

Installation
============

See the INSTALL file.  Apologies for its inadequacy.
