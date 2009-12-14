=ogBoumatic=

Wordpress theme by Owen Griffin based on the Boumatic theme by Allan Cole.

Designed for http://www.owengriffin.com/

==Requirements==

* Ruby
* Rake
* yuicompressor.jar
  You'll need to copy the yuicompressor.jar into the root folder of ogBoumatic
* SyntaxHighlighter
  Create a folder syntaxhighlighter/ and extract the latest syntax highlighter into
  into this folder.

==Building==

The default Rake task "all" will compress the CSS and Javascript

  rake all

You can also build just the CSS or just the JS

  rake style.js
  rake style.css

You can also deploy to a remote server using Rsync

  rake deploy



