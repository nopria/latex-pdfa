# Description
This repository contains all files required to produce PDF/A-2b compliant documents with a `pdflatex` workflow.

# Instructions
Switch to the **minimalexample** folder and compile with pdflatex the file `document.tex` to produce a sample PDF/A document.
Use `document.tex` as a template to create your own PDF/A document.

## Metadata

The file `*.xmpdata` must be present (though it can be empty) in source directory at the time that package `pdfx` is loaded. In the minimal example this is obtained by means of `\begin{filecontents*}` macro (in `document.tex` file), which creates the file `document.xmpdata` with the metadata specified in the lines between `\begin{filecontents*}` and `\end{filecontents*}`. ***Warning***: if you modify your metadata in your source tex file, you must remember to delete `*.xmpdata` before recompiling, since `*.xmpdata` is not rewrited and the resulting PDF/A will not reflect metadata changes.

### Symbols permitted in metadata

Within the metadata, all printable ASCII characters except `\`, `{`, `}`, and `%` represent themselves. Also, all printable Unicode characters from the basic multilingual plane (i.e., up to code point U+FFFF) can be used directly with the UTF-8 encoding. Consecutive whitespace characters are combined into a single space. Whitespace after a macro such as `\copyright`, `\backslash`, or `\sep` is ignored. Blank lines are ***not*** permitted. Moreover, the following markup can be used:

    '\ '          - a literal space  (for example after a macro)                  
    \%            - a literal '%'                                                 
    \{            - a literal '{'                                                 
    \}            - a literal '}'                                                 
    \backslash    - a literal '\'                                                 
    \copyright    - the (c) copyright symbol                                      

The macro `\sep` is only permitted within `\Author`, `\Keywords`, and `\Org`.  It is used to separate multiple authors, keywords, etc.

### List of supported metadata fields

Here is a list of user-definable metadata fields currently supported, and their meanings. More may be added in the future. You can refer to [documentation of `pdfx` package](http://ctan.mirror.garr.it/mirrors/CTAN/macros/latex/contrib/pdfx/pdfx.pdf#subsection.2.3) for a complete list.

- General information:
  
  |||
  |-|-|
  | `\Author{...}` | the document's human author. Separate multiple authors with `\sep` |
  | `\Title{...}`  | the document's title |
  | `\Keywords{...}` | list of keywords, separated with `\sep` |
  | `\Subject{...}` | the abstract |
  | `\Org{...}` | publishers |
  
- Copyright information:
  
  |||
  |-|-|
  | `\Copyright` | a copyright statement |
  | `\CopyrightURL` | location of a web page describing the owner and/or rights statement for this document |
  | `\Copyrighted` | `True` if the document is copyrighted, and `False` if it isn't. This is automatically set to `True` if either `\Copyright` or `\CopyrightURL` is specified, but can be overridden. For example, if the copyright statement is "Public Domain", this should be set to `False` |
  
- Publication information:
  
  |||
  |-|-|
  | `\PublicationType` | The type of publication. If defined, must be one of `book`, `catalog`, `feed`, `journal`, `magazine`, `manual`, `newsletter`, `pamphlet`. This is automatically set to `journal` if `\Journaltitle` is specified, but can be overridden |
  | `\Journaltitle` | The title of the journal in which the document was published |
  | `\Journalnumber` | The ISSN for the publication in which the document was published |
  | `\Volume` | Journal volume |
  | `\Issue` | Journal issue/number |
  | `\Firstpage` | First page number of the published version of the document |
  | `\Lastpage` | Last page number of the published version of the document |
  | `\Doi` | Digital Object Identifier (DOI) for the document, without the leading "doi:" |
  | `\CoverDisplayDate` | Date on the cover of the journal issue, as a human-readable text string |
  | `\CoverDate` | Date on the cover of the journal issue, in a format suitable for storing in a database field with a 'date' data type|

### Example of metadata

The following is an example of metadata (lines to insert between `\begin{filecontents*}` and `\end{filecontents*}` of `document.tex` file):  

    \Title{The Title Goes Here}
    \Author{Your Name Goes Here}
    \Copyright{Copyright \copyright\ 2014 "Author's Name Goes Here"}
    \Keywords{some keyword\sep another keyword\sep some more keywords}
    \Subject {This is where you put the abstract.}
