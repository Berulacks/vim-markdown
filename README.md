# Vim Github Markdown Support
... This is not ready by any means to be used, stay tuned :-)


# Why?
I wanted a strong support for the markdown flavour implemented by Github, I wanted a syntax highlight that would mirror the result I would find later on Github, I wanted a syntax highlight that would not break easily, I wanted a syntax highlight that I could rely on (aka rapid feedback), I wanted something more that a mere syntax highlight. The [Markdown Syntax](http://daringfireball.net/projects/markdown/syntax) unfortunately it's so loosely defined that there are *flavours* of markdown that are subtly incompatible from each other, the [Markdown supported by Github](https://help.github.com/articles/github-flavored-markdown) is one of them.


# Development
## Resources
* [Markdown Github Syntax](https://help.github.com/articles/github-flavored-markdown)
* [Markdown Github API](http://developer.github.com/v3/markdown)
* [Markdown Github Quick Preview](http://github-markdown-preview.heroku.com/)

## Syntax Specs
Testing syntax highlight could be tricky, here I use the golden master patter to at least avoid regressions, this is how it works: in `./rspec/features` you will find a bunch of `*.md` files, one for each syntactic element supported, for each of those files there's an html file, this file is created with the `:TOhtml` command and it's the reference (aka golden master) of the syntax highlight of the original file. Running `rspec` you are comparing the current syntax highlight of all the feature's file with the reference syntax highlight. If looking at some of the feature's file you see something wrong you can fix it and after regenerate the golden master files with `GENERATE_GOLDEN_MASTER=1 rspec`

# Documentation
I would use this section ultil I have a proper documentation for this plugin

## Motions
* `]]` start of the next header
* `[[` start of the previous header

## Editing
* when hitting `<Tab>`/`<S-Tab>` on a list item it will indent/unindent the item
* when hitting `<Tab>`/`<S-Tab>` on a blockquote it will increase/decrease the quote level
* when hitting `<Enter>` on a list item with no text in it (freshly created) it will delete the list item (aka everything till the column 0)
* when hitting `<C-\><Enter>` on a list item it will go to the next line on the same column as the first character of the line above

# BUGS
* look at spec/features/inline_links.md the last two examples, regions and nextgroup are not going to work here
* formatlistpat doesn't work for ordered lists
* enter doesn't select completion options anymore
* avoid effect of formatoptions with horizontal rules (asterisks and dashes)
* seems that iskeyword is not local?

# TODO
* mapping from `<C-\><Enter>` to `<Leader><Enter>`
* syntax
  * preformatted blocks
  * auto links
    * http://example.com) the closed parentesis should not be highlighted
    * http://example.com/(foo) should all be highlighted
  * links with references
  * images with references
  * todo lists (GFM)
* enable english spelling checking
* support tables if tabularize is installed
* emoticons (GFM)
  * start completion when hitting `:` in insert mode
  * remove duplication between syntax keywords and dictionary completion
  * more iabbr
* todo lists (GFM)
  * when on over todo item `<Leader><Space>` will check/uncheck it
* lists
  * when hitting `<BS>` on a list item with no text in it (freshly created) it will delete the list item (everything till the column 0)
  * when hitting `<C-K>` on a list item it will swap it with the item above (if it exists)
  * when hitting `<C-J>` on a list item it will swap it with the item below (if it exists)
* fenced code blocks (GFM)
  * open next quote level of a blockquote element in a scratch buffer
  * edit it with markdown syntax highlight
  * on exit copy the buffer's content back in the original file with the original quote level
  * explain in this file why I chose to avoid to highlight nested block elements
* custom text objects
  * list/todo item
  * paragraph
    * start of the next paragraph `}`
    * start of the previous paragraph `{`
  * inline elements
* tried to make strikethrough work without success but found [a patch](https://groups.google.com/d/msg/vim_use/xTXC-lk_pdc/Fe-TQzal_EMJ) wiil look into it another time
