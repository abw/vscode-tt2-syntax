# Template Toolkit Extension for Visual Studio Code

This implements a Visual Studio Code (vscode) extension providing syntax highlighting and snippets for Template Toolkit (TT2) template markup embedded in HTML files.

# File Extensions

The default file extensions that will be recognised as Template Toolkit files are `.tt` and `.ttml`.

# Syntax Highlighting

This extension identifies syntactic elements that are used in the Template Toolkit language and applies one or more scopes to the tokens that can then be targeted by a theme.

To inspect the scopes applied you can use the `Developer: Inspect Editor Tokens and Scopes` command available from the command palette.

For further information about Syntax Highlighting in VSCode see: https://code.visualstudio.com/api/language-extensions/syntax-highlight-guide

The syntactic elements and corresponding scopes are:

* Inline Tags - all tokens between `[%` and `%]` are given the `meta.tag.template.tt` scope.  The start and end tokens are also given this scope.

* Outline Tags - a line starting `%%` is given the `meta.tag.template.tt` scope until the end of line.  Note that you will need to define the `OUTLINE_TAG` Template Toolkit option if you want to use this.  e.g.

        my $tt = Template->new(
            OUTLINE_TAG => '%%',
        );

* Tag identifiers - the `[%` and `%]` markers for inline tags and the `%%` for outline tags are also given the `punctuation.definition.tag.tt` scope.

* Keywords - `IF`, `ELSE`, `END`, `INCLUDE`, `PROCESS`, etc., are given the `keyword.control.tt` scope.  Lower case variants of the keywords are also identified.  Note that you will need to set the `ANYCASE` Template Toolkit option if you want to use lower case keywords in your templates.

        my $tt = Template->new(
            ANYCASE => 1,
        );

* Operators - `+`, `-`, `<`, `>`, etc, are given the `keyword.operator.tt` scope.

* Variables - `foo`, `bar`, etc., are given the `variable.other.tt` scope.

* Double quoted string - `"like this"` are given the `string.quoted.double.tt` scope.  The opening and closing quote characters are also given the `punctuation.definition.string.begin.tt` and `punctuation.definition.string.end.tt` scopes, respectively.

* Single quoted strings - `'like this'` are given the `string.quoted.single.tt` scope.  The opening and closing quote characters are also given the `punctuation.definition.string.begin.tt` and `punctuation.definition.string.end.tt` scopes, respectively.

* Comments - `# like this` in a directive are given the `comment.line.number-sign.tt` scope.

# Snippets

The following snippets are provided in two different flavours.

The first uses the "traditional" syntax of inline tags with UPPER CASE keywords, e.g. `[% INCLUDE file %]`, for those of use who are old enough to remember what it was like to use computers before we had pretty colours and syntax highlighting and relied on UPPER CASE keywords to make things STAND OUT.

The second syntax uses lower case keywords and outline tags, e.g. `%% include file` for the more minimalist look.  You youngsters don't know how lucky you are.

## Traditional Syntax

These use the "traditional" syntax of UPPER CASE keywords embedded in inline tags.

### `ttif`

An `IF`/`END` directive using inline tags.

    [% IF condition %]
    content
    [% END %]

### `ttifel`

An `IF`/`ELSE`/`END` directive using inline tags.

    [% IF condition %]
    content
    [% ELSE %]
    content
    [% END %]

### `ttfor`

A `FOR`/`END` directive using inline tags.

    [% FOR var IN list %]
    content
    [% END %]

### `ttin`

An `INCLUDE` directive in an inline tag.

    [% INCLUDE file %]

### `ttpr`

A `PROCESS` directive in an inline tag.

    [% PROCESS file %]

### `ttwr`

A `WRAPPER`/`END` directive in inline tags.

    [% WRAPPER file %]
    content
    [% END %]

## Outline Syntax

These variations use outline tags and the "less shouty" lower case keywords.
Note that you will need to set the `OUTLINE_TAG` and `ANYCASE` Template Toolkit options in your Perl code for these to work.

    # in your Perl code
    my $tt = Template->new(
        OUTLINE_TAG => '%%',
        ANYCASE => 1,
    );

The prefixes are the same as for the inline/UPPER CASE snippets above, with an addiitonal `o` suffix, e.g. `ttwr` becomes `ttwro`.

### ttifo

An if/end directive using outline tags and lower case keywords

    %% if condition
    content
    %% end

### `ttifelo`

An `if`/`else`/`end` directive using outline tags and lower case keywords.

    %% if condition
    content
    %% else
    content
    %% end

### `ttforo`

A `for`/`end` directive using outline tags and lower case keywords.

    %% for var in list
    content
    %% end

### `ttino`

An `include` directive in an outline tag with lower case keyword.

    %% include file

### `ttpro`

A `process` directive in an outline tag with lower case keyword.

    %% process file

### `ttwro`

A `wrapper`/`end` directive in outline tags with lower case keywords

    %% wrapper file
    content
    %% end

