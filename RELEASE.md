# Release notes for version 5.1

## Improved block quotation facilities

The highlight of this release is an extension of the block
quotation facilities. When measuring the length of a quotation,
`\blockquote` and related commands can determine either the word
count or the number of lines. See the pointers in the changelog
for details.

# Release notes for version 5.0

## Backwards compatibility

This release introduces some changes which are not backwards
compatible out of the box. In order to ease the transition to the
new version, I've implemented a 'version' option which emulates
older versions of `csquotes`.

It is quite possible that you do not need to set this option at
all, even though you have older documents using `csquotes`. You
only need the 'version' option in older documents if:

  - you are using the `<punct>` argument of `\blockquote` and/or
  - you have redefined any of the old
     `\mk(pre|mid|fin)(text|block|disp)punct` hooks.

If these conditions do not apply and you run 5.0 with the default
settings, the output will be similar to 4.4. There is absolutely
no need to set `version=4.4` if you didn't use the old hooks and
the `<punct>` argument of `\blockquote` anyway.

I've also removed some legacy aliases. This is rather old stuff
from `csquotes` 3.x and even 2.x which has been marked as
depreciated for some time. Setting `version=4.4` will restore
them as well.

## Punctuation look-ahead

This release comes with a new punctuation look-ahead feature,
i.e., in addition to the `<punct>` argument of advanced quotation
commands like `\textquote`, these commands can now scan ahead for
trailing punctuation after their last argument and move it around
if desired.
   
This is required by quoting conventions such as the US quotation
style which requires that a period or a comma immediately after a
closing quotation mark be moved inside the quotes even if it is
not part of the quoted text.

The implementation of the look-ahead feature also implies a new
interpretation of the optional `<punct>` argument supported by
certain quotation commands. In previous version, the `<punct>`
argument was intended for terminal punctuation which is NOT part
of the quoted text. Starting with this release, it is intended
for punctuation which IS part of the quoted text (but may need to
be moved around).

The modified syntax is more intuitive to use because terminal
punctuation which is NOT part of the quoted text is simply placed
after the last argument of the command, i.e.:

    \textquote[citation][.]{quoted text}
   
becomes:
   
    \textquote[citation]{quoted text}.

All of this is discussed at length in the manual. See the
changelog in the manual for pointers to the relevant sections.

## Revised quotation hooks

The old quotation hooks:

    \mkpretextpunct
    \mkmidtextpunct
    \mkfintextpunct
    \mkpreblockpunct
    \mkmidblockpunct
    \mkfinblockpunct
    \mkpredisppunct
    \mkmiddisppunct
    \mkfindisppunct

have been removed and are replaced by new hooks:

    \mktextquote
    \mkblockquote
    \mkbegdispquote
    \mkenddispquote

which are much more powerful while being more intuitive to use.
If you have been using the old hooks in some documents, set
`version=4.4` to emulate the old interface.
