Package Control Messages
========================

MarkdownEditing
---------------

  # MarkdownEditing
  
  Markdown plugin for Sublime Text. Provides a decent Markdown color scheme (light and dark) with more __robust__ syntax highlighting and useful Markdown editing features for Sublime Text. 3 flavors are supported: Standard Markdown, __GitHub flavored Markdown__, MultiMarkdown.
  
  ![MarkdownEditing][LightTheme]
  
  [Dark][DarkTheme] and [Yellow][YellowTheme] and [ArcDark][ArcDarkTheme] theme available, plus [thirdparty themes](#additional-color-themes). See [configuration](#configuration) section to learn **how to change the theme**.
  
  ## Overview
  
  <!-- MarkdownTOC autolink="true" bracket="round" markdown_preview="markdown" -->
  
  - [Installation](#installation)
      - [Package Control](#package-control)
      - [Manual Installation](#manual-installation)
  - [Features](#features)
      - [Markdown features](#markdown-features)
      - [Wiki features](#wiki-features)
  - [Key Bindings](#key-bindings)
  - [GFM Specific Features](#gfm-specific-features)
  - [Commands for Command Palette](#commands-for-command-palette)
      - [General Commands](#general-commands)
      - [Links, References and Footnotes](#links-references-and-footnotes)
      - [Folding and Navigation](#folding-and-navigation)
  - [Configuration](#configuration)
      - [Additional color themes:](#additional-color-themes)
  - [Tips](#tips)
  - [Enable WYSIWYG](#enable-wysiwyg)
  - [Troubleshooting](#troubleshooting)
      - [Error loading syntax file...](#error-loading-syntax-file)
      - [Roll back to an older version](#roll-back-to-an-older-version)
  - [Related Plugins](#related-plugins)
  - [Known Bugs](#known-bugs)
  - [Contributing](#contributing)
  - [Credits](#credits)
  - [Donation](#donation)
  - [License](#license)
  
  <!-- /MarkdownTOC -->
  
  ## Installation
  
  You can install MarkdownEditing either from Package Control (recommended) or manually. Package Control automatically download the package and keeps it up-to-date. Manual installation is required if you need to tweak the code.
  
  If you are using Sublime Text 2, you have to disable the native package _manually_. To do that, add `Markdown` to your `ignored_packages` list in ST user settings:
  
      "ignored_packages": [..., "Markdown"],
  
  > Getting "Error loading syntax file..."? See [this](#error-loading-syntax-file).
  
  ### Package Control
  
  The preferred method of installation is via [Sublime Package Control][PackageControl].
  
  1. [Install Sublime Package Control][InstallPackageControl]
  2. From inside Sublime Text, open Package Control's Command Pallet: <kbd>CTRL</kbd> <kbd>SHIFT</kbd> <kbd>P</kbd> (Windows, Linux) or <kbd>CMD</kbd> <kbd>SHIFT</kbd> <kbd>P</kbd> on Mac.
  3. Type `install package` and hit Return. A list of available packages will be displayed.
  4. Type `MarkdownEditing` and hit Return. The package will be downloaded to the appropriate directory.
  5. Restart Sublime Text to complete installation. Open a Markdown file and this custom theme. The features listed below should now be available.
  
  ### Manual Installation
  
  1. In Sublime Text, open the menu "Preferences" -> "Browse Packages...". This is the Sublime Text Packages directory.
  2. [Download and unzip](https://github.com/SublimeText-Markdown/MarkdownEditing/archive/master.zip) or [clone](https://help.github.com/articles/cloning-a-repository/) this repository to a directory `MarkdownEditing` in the Sublime Text Packages directory.
  3. The folder structure should look like `.../Sublime Text 3/Packages/MarkdownEditing/[files]`.
  4. Restart Sublime Text to complete installation. Open a Markdown file. The features listed below should now be available.
  
  ## Features
  
  You can access most features through Command Palette. You can launch it from `Tools -> Command Palette...`. MarkdownEditing commands start with `MarkdownEditing:`. And they are only visible when a markdown file is open and active.
  
  ### Markdown features
  
  * __Pairing__
      - Asterisks and underscores are autopaired and will wrap selected text.
      - If you start an empty pair and hit backspace, both elements are deleted.
      - If you start an empty pair and hit space, the right element is deleted.
      - Backticks are paired. So entering `` ` `` will expand to `` `(cursor here)` ``.
  * __List__
      - At the end of a list item, pressing <kbd>Enter</kbd> will automatically insert the new list item bullet.
      - Pressing <kbd>Tab</kbd> on the blank list item will indent it and switch the list bullet to another one (Order is `*`, `-`, `+` in a cycle).
      - Pressing <kbd>Shift</kbd> <kbd>Tab</kbd> on the blank list item will unindent it in the same way as above.
      - Sequential <kbd>Tab</kbd> s or <kbd>Shift</kbd> <kbd>Tab</kbd> s are supported.
      - You can disable automatic bullet switching or choose which bullets to be used, in your settings file (`mde.list_indent_bullets`).
      - If a list item contains a [GFM task][], pressing <kbd>Enter</kbd> at the end of the line will continue with a new blank task.
  * __Blockquote__
      - At the end of a blockquote line, pressing <kbd>Enter</kbd> will automatically extend blockquote.
      - Selecting some text and pressing <kbd>&gt;</kbd> will convert it to blockquote. The first and the last line don't have to be fully selected; partial select works, too.
  * __Link__
      - Left bracket pairing is modified to eliminate the selection and leave the cursor at a point where you can insert a `[]` or `()` pair for a link.
      - If you leave the cursor on a link, you can right click and jump between reference and url.
  * __Navigation__
      - Displays Markdown headers in the Project Symbol List (`Goto -> Goto Symbol in Project...`). They will start with `#`, so you will know they belong to markdown files at a glance. Also they will be on top of the list because of the precedence of `#`.
      - Headers also appear in Document Symbol List (`Goto -> Goto Symbol...`)
      - You can fold current section with <kbd>Ctrl</kbd> <kbd>Tab</kbd>
      - You can navigate between adjacent headers with `Find Next(Previous) Heading` command.
  * __Strikethrough__
      - <kbd>~</kbd> wraps selected text with `~~` (strikethrough). When you for instance select the word "foo" and hit  `~`, the result will be `~~foo~~`.
  * __Header__
      - Typing `#` when there's a selection will surround it with `#` to make it a headline. Multiple presses add additional hashes, increasing the level of the header. Once you hit 6 hashes, it will reset to 0 on the next press. The `mde.match_header_hashes` will determine if the `#` are mirrored on both sides or just at the beginning of the line.
      - Typing return at the end of a line that begins with hashmarks will insert closing hashmarks on the headline. They're not required for Markdown, it's just aesthetics, and you can change the `mde.match_header_hashes` option in your settings to enable (disabled by default).
      - Setext-style headers can be completed with `Tab`. That is, typing `Tab` on a line containing only `=` or `-` characters will add or remove enough characters to it to match the length of the line above.
      - New documents will be named automatically based on the first header.
  
  ### Wiki features
  
  Wiki links are defined by surrounding a (wiki) word with double square brackets, for example:
  
      [[SampleWikiPage]]
  
  The user can `open` wiki page using a sublime command.  This will search the current open file's directory (and sub-directories) for a file with a matching name and a markdown extension.  For example, opening the previous wiki link
  will look for and open a file named:
  
      SampleWikiPage.md
  
  Note that, if the wiki page does *not* yet exist, if will be created with a header matching the page name.  However the file will only actually be created on the file system, when it is saved by the user.  
  
  The user can `list back links` and of course to open them.  Back links are pages that reference the current page.  This allows pages to be tied together into a personal wiki.   A common technique is to define *tag* wiki pages and to list any tags for a page as references to the tag pages at the bottom of the page, for example:
      
      [[TagSyntax]] [[TagDev]] [[TagPython]]
  
  This allows the user to list all pages with a specific tag, by opening the tag page and list all back links.
  
  Journal wiki pages are also supported.  A journal page is just a wiki page with a name matching the current date.
  
  Lastly the command to open the *home* page is provided, where the home page is just a wiki page named `HomePage`.
  
  ## Key Bindings
  
  | OS X | Windows/Linux | Description |
  |------|---------------|-------------|
  | <kbd>⌘</kbd><kbd>⌥</kbd><kbd>V</kbd> | <kbd>Ctrl</kbd><kbd>Alt</kbd><kbd>V</kbd> | Creates or pastes the contents of the clipboard as an inline link on selected text.
  | <kbd>⌘</kbd><kbd>⌥</kbd><kbd>R</kbd> | <kbd>Ctrl</kbd><kbd>Alt</kbd><kbd>R</kbd> | Creates or pastes the contents of the clipboard as a reference link.
  | <kbd>⌘</kbd><kbd>⇧</kbd><kbd>K</kbd> | <kbd>Shift</kbd><kbd>Win</kbd><kbd>K</kbd> | Creates or pastes the contents of the clipboard as an inline image on selected text.
  | <kbd>⌘</kbd><kbd>⌥</kbd><kbd>B</kbd> <kbd>⌘</kbd><kbd>⌥</kbd><kbd>I</kbd> | <kbd>Alt</kbd><kbd>B</kbd> <kbd>Alt</kbd><kbd>I</kbd> | These are bound to bold and italic. They work both with and without selections. If there is no selection, they will just transform the word under the cursor. These keybindings will unbold/unitalicize selection if it is already bold/italic.
  | <kbd>⌘</kbd><kbd>^</kbd><kbd>1...6</kbd> | <kbd>Ctrl</kbd><kbd>1...6</kbd> | These will add the corresponding number of hashmarks for headlines. Works on blank lines and selected text in tandem with the above headline tools. If you select an entire existing headline, the current hashmarks will be removed and replaced with the header level you requested. This command respects the `mde.match_header_hashes` preference setting.
  | <kbd>⌥</kbd><kbd>⇧</kbd><kbd>6</kbd> | <kbd>Alt</kbd><kbd>Shift</kbd><kbd>6</kbd> | Inserts a footnote.
  | <kbd>⇧</kbd><kbd>Tab</kbd> | <kbd>Shift</kbd><kbd>Tab</kbd> | Fold/Unfold current section.
  | <kbd>^</kbd><kbd>⇧</kbd><kbd>Tab</kbd> | <kbd>Ctrl</kbd><kbd>Shift</kbd><kbd>Tab</kbd> | Fold all sections under headings of a certain level.
  | <kbd>⌘</kbd><kbd>⌥</kbd><kbd>PageUp</kbd> <kbd>⌘</kbd><kbd>⌥</kbd><kbd>PageDown</kbd> | <kbd>Ctrl</kbd><kbd>Alt</kbd><kbd>Shift</kbd><kbd>PageUp</kbd> <kbd>Ctrl</kbd><kbd>Alt</kbd><kbd>Shift</kbd><kbd>PageDown</kbd> | Go to the previous/next heading of the same or higher level
  | <kbd>⌘</kbd><kbd>⇧</kbd><kbd>PageUp</kbd> <kbd>⌘</kbd><kbd>⇧</kbd><kbd>PageDown</kbd> | <kbd>Ctrl</kbd><kbd>Shift</kbd><kbd>PageUp</kbd> <kbd>Ctrl</kbd><kbd>Shift</kbd><kbd>PageDown</kbd> |  Go to the previous/next heading
  | <kbd>⌘</kbd><kbd>⌥</kbd><kbd>H</kbd> | <kbd>Ctrl</kbd><kbd>Shift</kbd><kbd>H</kbd> | Open home page
  | <kbd>⌘</kbd><kbd>⌥</kbd><kbd>D</kbd> | <kbd>Ctrl</kbd><kbd>Shift</kbd><kbd>D</kbd> | Open wiki page under the cursor
  | <kbd>⌘</kbd><kbd>⌥</kbd><kbd>J</kbd> | <kbd>Ctrl</kbd><kbd>Shift</kbd><kbd>J</kbd> | Open journal page for today
  | <kbd>⌘</kbd><kbd>⌥</kbd><kbd>B</kbd> | <kbd>Ctrl</kbd><kbd>Shift</kbd><kbd>B</kbd> | List back links
  
  
  ## GFM Specific Features
  
  [GFM][] means GitHub Flavored Markdown is the dialect of Markdown that is currently supported for user content on GitHub.com and GitHub Enterprise. It has [some unique features][GFMFeatures]:
  
  Underscores in words doesn't mess with bold or italic style:
  
  ![underscore-in-words][GFM-UnderscoreInWords]
  
  Fenced code blocks gets syntax highlighting inside:
  
  ![fenced-code-block][GFM-FencedCodeBlock]
  
  Keyboard shortcuts gets highlighted like in GitHub:
  
  ![keyboard-shortcut][GFM-KeyboardShortcut]
  
  Strikethrough is supported:
  
  ![strikethrough][GFM-Strikethrough]
  
  ## Commands for Command Palette
  
  You can launch Command Palette from `Tools -> Command Palette...`. MarkdownEditing commands start with `MarkdownEditing:`. And they are only visible when a markdown file is open and active.
  
  ### General Commands
  
  * __Fix Underlined Headers__
      Adjusts every setext-style header to add or remove `=` or `-` characters as needed to match the lengths of their header text.
  * __Convert Underlined Headers to ATX__
      Converts every setext-style header into an ATX style header. If something is selected only the headers in the selections will be converted, otherwise the conversion will be applied to the whole view.
  * __Markdown Lint__
      Performs lint on current Markdown file using a local linter. See [lint rules](lint_docs/RULES.md). Some of the linting rules are customizable via user settings file.
  * __Run markdownlint__
      Run mdl command from [markdownlint](https://github.com/markdownlint/markdownlint) package. You need to install it by yourself.
  * __Change color scheme...__
      Lists built-in Markdown color schemes for you to preview and use.
  * __Switch List Bullet Type__
      Switches the highlighted list between numbered and bulleted style.
  
  ### Links, References and Footnotes
  
  * __Add Missing Link Labels__
      Scans document for referenced link usages (`[some link][some_ref]` and `[some link][]`) and checks if they are all defined. If there are undefined link references, command will automatically create their definition snippet at the bottom of the file.
  * __Magic Footnotes Command__
      Adds a footnote after the word under cursor. If cursor is already on a footnote, jumps to its definition or reference.
  * __Gather Missing Footnotes__
      Add definition stubs (if there is none) for all footnotes references.
  * __Jump Reference__
      Jumps cursor between definitions and references.
  * __New Reference__
      Adds a new link under cursor.
  * __New Inline Link__
      Adds a new inline link under cursor.
  * __New Inline Image__
      Adds a new inline image under cursor.
  * __New Image__
      Adds a new image under cursor.
  * __New Footnote__
      Adds a footnote under cursor.
  * __Delete Reference__
      Deletes the definition and references of a link.
  * __Organize References__
      Sorts and gives a report on current link references usage.
  
  ### Folding and Navigation
  
  Remeber you can <kbd>Ctrl</kbd> <kbd>R</kbd> (in document) and <kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>R</kbd> (project-wise) for quick navigation for all headers.
  
  * __Toggle Folding Current Section__
      Folds/unfolds current section.
  * __Fold Level 1-4 Sections__
      Fold all sections under headers of specific level.
  * __Fold/Unfold All Sections__
      Self explanatory.
  * __Find Next/Previous Heading__
      You have option to find just same or higher level or any level
  
  ## Configuration
  
  The plugin contains 3 different Markdown flavors: Standard Markdown, GitHub flavored Markdown, MultiMarkdown. Default is GitHub flavored Markdown. If you want to set another one as default, open a Markdown file and select your flavor from the menu: `View > Syntax > Open all with current extension as`. You're done.
  
  You may want to have a look at the default settings files. They are located at:
  
      Packages/MarkdownEditing/Markdown.sublime-settings         [GitHub flavored Markdown]
      Packages/MarkdownEditing/Markdown (Standard).sublime-settings
      Packages/MarkdownEditing/MultiMarkdown.sublime-settings
  
  If you want to override any of the default settings, you can open the appropriate user settings file using the `Preferences > Package Settings > Markdown Editing` menu. Each flavor has a different settings file.
  
  Bold and italic markers are configurable through ST shell variables. You can use `Preferences > Package Settings > Markdown Editing` menu to see the default settings file. In order to override it, copy & paste its content into the user settings file (`Packages/User/Bold and Italic Markers.tmPreferences`) from the menu and make your edits. It is pretty straightforward.
  
  In order to activate the dark or the yellow theme, put one of these lines to your user settings file of the flavor (`Packages/User/[flavor].sublime-settings`):
  
      "color_scheme": "Packages/MarkdownEditing/MarkdownEditor-Dark.tmTheme",
      "color_scheme": "Packages/MarkdownEditing/MarkdownEditor-Yellow.tmTheme",
      "color_scheme": "Packages/MarkdownEditing/MarkdownEditor-ArcDark.tmTheme",
      
  
  If you want to go with your already existing theme, you can reenable it with the same method as above. Keep in mind that, that theme may not cover all the parts of the Markdown syntax that this plugin defines.
  
  ### Additional color themes:
  
  - [Blackboard theme][linkBlackboardTheme] by [@mdesantis][mdesantis]
  - [monokaiC](https://github.com/avivace/monokaiC) by [@avivace][avivace]
  
  By default, when you install the plugin, files with these extensions will be assigned to Markdown syntax: "md", "txt", "mdown", "markdown", "markdn". If you want to prevent any of these extensions to be opened as Markdown, follow these steps:
  
  1. Click on the language menu at bottom right
  2. Select "Open all with current extension as"
  3. Choose your preferred syntax for that extension
  
  ## Tips
  
  We are maintaining a [tips section][tips] in our [Wiki][]. Jump there to learn from others or share your experiences with others.
  
  ## Enable WYSIWYG
  
  Sublime can be configured into a WYSIWYG (what you see is what you get) editor with two other plugins:
  
  1. Markdown Preview (https://packagecontrol.io/packages/Markdown%20Preview)
  1. Livereload (https://packagecontrol.io/packages/LiveReload)
  
  Install them if you haven't. Then
  
  1. Open Palette
  1. LiveReload: Enable/Disable Plugins
  1. Enable Simple Reload.
  
  Now open palette and choose "Preview in Browser" and you will get a WYSIWYG editor.
  
  ## Troubleshooting
  
  ### Error loading syntax file...
  
  __Are you getting this error after installation: _**Error loading syntax file** "Packages/Markdown/Markdown.tmLanguage": Unable to open Packages/Markdown/Markdown.tmLanguage_?__
  
  >  This is caused by open markdown files at the install time. You have to __manually change their syntax to your newly installed Markdown syntax__. Read the below paragraph for more details on this.
  
  _Note_: Sublime text has a native tiny package for Markdown. However, when MarkdownEditing is enabled, native package causes some conflicts. For this reason, MarkdownEditing will automatically disable it. Since it doesn't bring anything new over MarkdownEditing, this is not a loss. But remember, when you disable MarkdownEditing, you have to reenable the native one manually (if you want).
  
  ### Roll back to an older version
  
  When you notice any undesired behavior introduced by the latest update, your feedback is always welcome in our [issue page](https://github.com/SublimeText-Markdown/MarkdownEditing/issues). However before it's fixed, you can rollback to [an earlier version](https://github.com/SublimeText-Markdown/MarkdownEditing/releases). Find the desired version and download the zip file, then follow [manual installation guide](#manual-installation)
  
  ## Related Plugins
  
  * [Knockdown][]
  
       Knockdown offers useful Markdown features and a custom Markdown theme. All of its unique features except its theme are ported to MarkdownEditing and some of them are actually improved further in MarkdownEditing.
  * [Sublime Markdown Extended][]
  * [SmartMarkdown][]
  * [MarkdownTOC][]
      - Sublime Text 3 plugin for generating a Table of Contents (TOC) in a Markdown document.
  * See https://packagecontrol.io/search/markdown for more.
  
  ## Known Bugs
  
  * Setext-style headers (`===` and `---`) do not show up in the symbol list. This is due to a Sublime Text limitation (see [#158][]). However, we are able to put a placeholder to indicate the existence of the header. We encourage you to use Atx-style headers (`#`).
  
  * Installing for the first time while having markdown files opened may cause MarkdownEditing to behave unexpectedly on those files. Close and reopen those files to fix it.
  
  ## Contributing
  
  See `CONTRIBUTING.md` file.
  
  ## Credits
  
  MarkdownEditing was originally created by [Brett Terpstra][brettterpstra] and has become a community project with the goal of consolidating the best features from the varied collection of Markdown packages for Sublime Text. Current development is headed up by [Ali Ayas][maliayas] and [Felix Hao][felixhao28].
  
  Related blog posts from Brett:
  * http://brettterpstra.com/2012/05/17/markdown-editing-for-sublime-text-2-humble-beginnings/
  * http://brettterpstra.com/2013/11/23/markdownediting-for-sublime-text-updates/
  
  This plugin contains portions of code from [Knockdown][].
  
  Footnote commands were submitted by [J. Nicholas Geist][] and originated at [geekabouttown][geekabouttown].
  
  ## Donation
  
  You can support [contributors](https://github.com/SublimeText-Markdown/MarkdownEditing/graphs/contributors) of this project individually. Every contributor is welcomed to add his/her line below with any content. Ordering shall be alphabetically by GitHub username.
  
  * [@felixhao28][felixhao28]: <a href="https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=9QV2RFV2J8UZS"><img src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" alt="[paypal]" /></a>
  * [@maliayas][maliayas]: <a href="https://www.paypal.com/cgi-bin/webscr?cmd=_donations&amp;business=W2NXRPD43YSCU&amp;lc=TR&amp;item_name=open-source&amp;item_number=markdown-editing&amp;currency_code=USD&amp;bn=PP%2dDonationsBF%3abtn_donate_LG%2egif%3aNonHosted"><img src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" alt="[paypal]" /></a> ![donation received](http://maliayas.com/business/donation/badge.php?project=markdown_editing)
  
  ## License
  
  MarkdownEditing is released under the [MIT License][opensource].
  
  [LightTheme]: https://raw.github.com/SublimeText-Markdown/MarkdownEditing/master/screenshots/light.png
  [DarkTheme]: https://raw.github.com/SublimeText-Markdown/MarkdownEditing/master/screenshots/dark.png
  [YellowTheme]: https://raw.github.com/SublimeText-Markdown/MarkdownEditing/master/screenshots/yellow.png
  [ArcDarkTheme]: https://raw.github.com/SublimeText-Markdown/MarkdownEditing/master/screenshots/arcdark.png
  [PackageControl]: http://wbond.net/sublime_packages/package_control
  [InstallPackageControl]: http://wbond.net/sublime_packages/package_control/installation
  [GFM task]: https://github.github.com/gfm/#task-list-items-extension-
  [GFM]: https://github.github.com/gfm/
  [GFMFeatures]: https://guides.github.com/features/mastering-markdown/
  [GFM-UnderscoreInWords]: https://raw.github.com/SublimeText-Markdown/MarkdownEditing/master/screenshots/underscore-in-words.png
  [GFM-FencedCodeBlock]: https://raw.github.com/SublimeText-Markdown/MarkdownEditing/master/screenshots/fenced-code-block.png
  [GFM-KeyboardShortcut]: https://raw.github.com/SublimeText-Markdown/MarkdownEditing/master/screenshots/keyboard-shortcut.png
  [GFM-Strikethrough]: https://raw.github.com/SublimeText-Markdown/MarkdownEditing/master/screenshots/strikethrough.png
  [linkBlackboardTheme]: https://github.com/mdesantis/MarkdownEditing/blob/blackboard-theme/MarkdownEditor-Blackboard.tmTheme
  [mdesantis]: https://github.com/mdesantis
  [avivace]: https://github.com/avivace
  [tips]: https://github.com/SublimeText-Markdown/MarkdownEditing/wiki/Tips
  [Wiki]: https://github.com/SublimeText-Markdown/MarkdownEditing/wiki
  [Knockdown]: https://github.com/aziz/knockdown/
  [Sublime Markdown Extended]: https://github.com/jonschlinkert/sublime-markdown-extended
  [SmartMarkdown]: https://github.com/demon386/SmartMarkdown
  [MarkdownTOC]: https://github.com/naokazuterada/MarkdownTOC
  [#158]: https://github.com/SublimeText-Markdown/MarkdownEditing/issues/158
  [brettterpstra]: http://brettterpstra.com
  [maliayas]: https://github.com/maliayas
  [felixhao28]: https://github.com/felixhao28
  [J. Nicholas Geist]: https://github.com/jngeist
  [geekabouttown]: http://geekabouttown.com/posts/sublime-text-2-markdown-footnote-goodness
  [opensource]: http://www.opensource.org/licenses/MIT


Markdown Preview
----------------

  Sublime Text 2/3 Markdown Preview
  =================================
  
  Preview and build your markdown files quickly in your web browser from sublime text 2/3. 
  
  You can use builtin [python-markdown][10] parser or use the [github markdown API][5] for the conversion.
  
  **NOTE:** If you choose the GitHub API for conversion (set parser: github in your settings), your code will be sent through https to github for live conversion. You'll have [Github flavored markdown][6], syntax highlighting and EMOJI support for free :heart: :octocat: :gift:. If you make more than 60 calls a day, be sure to set your GitHub API key in the settings :). You can also get most of this in the default Markdown parser with by enabling certain extensions; see "[Parsing Github Flavored Markdown](#parsing-github-flavored-markdown-)"" below for more information.
  
  **LINUX users:** If you want to use GitHub API for conversion, you'll need to have a custom Python install that includes python-ssl as its not built in the Sublime Text 2 Linux package. see [@dusteye comment][8]. If you use a custom window manager, also be sure to set a `BROWSER` environment variable. see [@PPvG comments][9]
  
  ## Features :
  
   - Markdown preview using the [Python-markdown][10] or the Github API just choose select the build commands.
   - Syntax highlighting via Pygments. See "[Configuring Pygments](#configuring-pygments)" for more info.
   - Build markdown file using Sublime Text build system. The build parser are config via the `"parser"` config.
   - Browser preview auto reload on save if you have the [ST LiveReload plugin][7] installed.
   - Builtin parser : supports `abbr`, `attr_list`, `def_list`, `fenced_code`, `footnotes`, `tables`, `smart_strong`, `smarty`,  `wikilinks`, `meta`, `sane_lists`, `codehilite`, `nl2br`, and `toc` markdown extensions.
   - CSS search path for local and build-in CSS files (always enabled) and/or CSS overriding if you need
   - YAML support thanks to @tommi
   - Clipboard selection and copy to clipboard thanks to @hexatrope
   - MathJax support : \\\\(\frac{\pi}{2}\\\\) thanks to @bps10. You have to set `enable_mathjax` to `true` in your settings. MathJax is then downloaded in the background so you need to have an internet access.
   - HTML template customisation thanks to @hozaka
   - Embed images as base64 (see [settings][settings] file for more info)
   - Strip out multimarkdown critic marks from either Githubs or Python Markdown input source (see [settings][settings] file for more info)
   - 3rd party extensions for the Python Markdown parser:
  
      | Extension | Documentation |
      |-----------|---------------|
      | magiclink | Find and convert HTML links and email address to links ([MagicLink Documentation](http://facelessuser.github.io/pymdown-extensions/extensions/magiclink/)). |
      | delete | Surround inline text with `~~strike through~~` to get del tags ~~strike through~~. |
      | insert | Surround inline text with `^^underlined^^` to get ins tags <ins>underlined</ins>. |
      | tasklist | Github Flavored Markdown tasklists ([Tasklist Documentation](http://facelessuser.github.io/pymdown-extensions/extensions/tasklist/)). |
      | githubemoji | Support for Github Flavored Markdown emojis ([GithubEmoji Documentation](http://facelessuser.github.io/pymdown-extensions/extensions/githubemoji/)). |
      | headeranchor | Github Flavored Markdown style header anchors ([HeaderAnchor Documentation](http://facelessuser.github.io/pymdown-extensions/extensions/headeranchor/)). |
      | github | A convenience extension to add: `magiclink`, `delete`, `tasklist`, `githubemoji`, `headeranchor`, `superfences`, and `nl2br` to parse and display Markdown in a github-ish way.  It is recommed to pair `github` with `extra` and `codehilite` (with language guessing off) to parse close to github's way.  Be aware of what extensions `github` loads, because you should not load extensions more than once. |
      | progressbar | Create progress bars ([ProgressBar Documentation](http://facelessuser.github.io/pymdown-extensions/extensions/progressbar/)). |
      | superfences | Allow fenced blocks to be nested under lists, blockquotes, etc. and add special UML diagram blocks ([SuperFences Documentation](http://facelessuser.github.io/pymdown-extensions/extensions/superfences/)). |
  
  ## Installation :
  
  ### Using [Package Control][3] (*Recommended*)
  
  For all Sublime Text 2/3 users we recommend install via [Package Control][3].
  
  1. [Install][11] Package Control if you haven't yet.
  2. Use <kbd>cmd</kbd>+<kbd>shift</kbd>+<kbd>P</kbd> then `Package Control: Install Package`
  3. Look for `Markdown Preview` and install it.
  
  ### Manual Install
  
  1. Click the `Preferences > Browse Packages…` menu
  2. Browse up a folder and then into the `Installed Packages/` folder
  3. Download [zip package][12] rename it to `Markdown Preview.sublime-package` and copy it into the `Installed Packages/` directory
  4. Restart Sublime Text
  
  ## Usage :
  
  ### To preview :
  
   - optionally select some of your markdown for conversion
   - use <kbd>cmd</kbd>+<kbd>shift</kbd>+<kbd>P</kbd> then `Markdown Preview` to show the follow commands (you will be prompted to select which parser you prefer):
  	- Markdown Preview: Preview in Browser
  	- Markdown Preview: Export HTML in Sublime Text
  	- Markdown Preview: Copy to Clipboard
  	- Markdown Preview: Open Markdown Cheat sheet
   - or bind some key in your user key binding, using a line like this one:
     `{ "keys": ["alt+m"], "command": "markdown_preview", "args": {"target": "browser", "parser":"markdown"} },` for a specific parser and target or `{ "keys": ["alt+m"], "command": "markdown_preview_select", "args": {"target": "browser"} },` to bring up the quick panel to select enabled parsers for a given target.
  
  ### Live Reload
  
  To get live updates while editing a file after preview, you need to do the following:
  
  1. enable the `enable_autoreload` setting in `MarkdownPreview.sublime-settings`.
  2. Install [LiveReload][7] package from Package Control.
  3. Restart.
  4. Open the command palette and select the command `LiveReload: Enable/disable plug-ins`.
  5. Select `Simple Reload with delay (400ms)`.  It is possible you can get away with `Simple Reload`, but some experience an issue where they are one rev behind when using `Simple Reload`.
  6. Edit document and enjoy live reload.
  
  You don't need to enable `Simple Reload` on every file.  Once is enough.  New files should auto-reload when you open them in the browser.
  
  ### Enabling Other External Markdown Parsers :
  
  External parser commands and arguments should first be mapped to a name.  The path to the binary should be first, followed by flags etc.
  
  ```js
      "markdown_binary_map": {
          "multimarkdown": ["/usr/local/bin/multimarkdown"]
      },
  ```
  
  Then the name can be placed in `enabled_parsers` to enable use of the new parser.
  
  ```js
      "enabled_parsers": ["markdown", "github", "multimarkdown"],
  ```
  
  ### To build :
  
   - Just use <kbd>ctrl</kbd>+<kbd>B</kbd> (Windows/Linux) or <kbd>cmd</kbd>+<kbd>B</kbd> (Mac) to build current file.
  
  ### To config :
  
  Using Sublime Text menu: `Preferences`->`Package Settings`->`Markdown Preview`
  
  - `Settings - User` is where you change your settings for Markdown Preview.
  - `Settings - Default` is a good reference with detailed descriptions for each setting.
  
  ### Configuring Pygments
  If you add the codehilite extension manually in the enabled extensions, you can override some of the default settings.
  
  * Turn language guessing *on* or *off* (*on* will highlight fenced blocks even if you don't specify a language)  `codehilite(guess_lang=False)` (True|False).
  * Show line numbers: `codehilite(linenums=True)` (True|False).
  * Change the higlight theme: `codehilite(pygments_style=emacs)`.
  * Inline the CSS: `codehilite(noclasses=True)` (True|False).
  * Use multiple: `codehilite(linenums=True, pygments_style-emacs)`.
  
  See [codehilte page](https://pythonhosted.org/Markdown/extensions/code_hilite.html) for more info.
  
  ### Meta Data Support
  When the `meta` extension is enabled (https://pythonhosted.org/Markdown/extensions/meta_data.html), the results will be written to the HTML head in the form `<meta name="key" content="value1,value2">`.  `title` is the one exception, and its content will be written to the title tag in the HTML head.
  
  ### YAML Frontmatter Support
  YAML frontmatter can be stripped out and read when `strip_yaml_front_matter` is set to  `true` in the settings file.  In general the, the fronmatter is handled the same as [meta data](#meta-data-support), but if both exist in a file, the YAML keys will override the `meta` extension keys.  There are a few special keys names that won't be handled as html meta data.
  
  #### Special YAML Key Names
  Yaml frontmatter has a few special key names that are used that will not be handled as meta data:
  
  - **basepath**: An absolute path to configure the relative paths for images etc. (for when the markdown is supposed to reference images in a different location.)
  - **references**: Can take a file path or an array of file paths for separate markdown files containing references, footnotes, etc.  Can be an absolute path or relative path.  Relative paths first use the source file's directory, and if the file cannot be found, it will use the `basepath` setting.
  - **destination**: This is an absolute file path or relative file path for when the markdown is saved to html via the build command or the `Save to HTML` command.  Relative paths first use the source file's directory, and if the file cannot be found, it will use the `basepath` setting.
  - **settings**: This is a dictionary where you can override settings that are in the settings file.
  
  #### Example
  ```yaml
  ---
      # Builtin values
      references:
          - references.md
          - abbreviations.md
          - footnotes.md
  
      destination: destination.html
  
      # Meta Data
      title: Test Page
      author:
          - John Doe
          - Jane Doe
  
      # Settings overrides
      settings:
          enabled_extensions:
          - extra
          - github
          - toc
          - headerid
          - smarty(smart_quotes=False) # smart quotes interferes with attr_list
          - meta
          - wikilinks
          - admonition
          - codehilite(guess_lang=False,pygments_style=github)
  ---
  ```
  
  ### Parsing Github Flavored Markdown :
  Github Flavored Mardown (GFM) is a very popular markdown.  Markdown Preview can actually handle them in a couple of ways: online and offline.
  
  #### Online :
  Parsing GFM using the online method requires using the Github API as the parser.  It may also require setting `github_mode` to `gfm` to get things like tasklists to render properly. You can set your API key in the settings as follows:
  
  ```js
      "github_oauth_token": "secret"
  ```
  
  #### Offline :
  By default almost all extensions are enabled to help with the github feel, but there are some tweaks needed to get the full experience.
  
  GFM does not auto guess language in fenced blocks, but Markdown Preview does this by default.  You can fix this in one of two ways:
  
  1. Disable auto language guessing in the settings file `"guess_language": false,`
  2. Or if you are manually defining extensions: `"enabled_extensions": ["codehilite(guess_lang=False,pygments_style=github)"]`
  
  
  As mentioned earlier, almost all extensions are enabled by default, but as a reference, the minimum extensions that should be enabled are listed below:
  
  ```javascript
  	"enabled_extensions": [
  		"extra",
  		"github",
  		"codehilite(guess_lang=False,pygments_style=github)"
  	]
  ```
  
  This may be further enhanced in the future.
  
  
  ## Support :
  
  - Any bugs about Markdown Preview please feel free to report [here][issue].
  - And you are welcome to fork and submit pull requests.
  
  
  ## License :
  
  The code is available at github [project][home] under [MIT license][4].
  
   [home]: https://github.com/revolunet/sublimetext-markdown-preview
   [3]: https://packagecontrol.io/
   [4]: http://revolunet.mit-license.org
   [5]: https://developer.github.com/v3/markdown/
   [6]: https://help.github.com/articles/github-flavored-markdown/
   [7]: https://github.com/Grafikart/ST3-LiveReload
   [8]: https://github.com/revolunet/sublimetext-markdown-preview/issues/27#issuecomment-11772098
   [9]: https://github.com/revolunet/sublimetext-markdown-preview/issues/78#issuecomment-15644727
   [10]: https://github.com/waylan/Python-Markdown
   [11]: https://packagecontrol.io/installation
   [12]: https://github.com/revolunet/sublimetext-markdown-preview/archive/master.zip
   [issue]: https://github.com/revolunet/sublimetext-markdown-preview/issues
   [settings]: https://github.com/revolunet/sublimetext-markdown-preview/blob/master/MarkdownPreview.sublime-settings
