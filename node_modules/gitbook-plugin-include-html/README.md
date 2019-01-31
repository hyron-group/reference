# gitbook-plugin-include-html

✳️✳️ Forked from [gitbook-plugin-include](https://github.com/rlmv/gitbook-plugin-include) ✳️✳️


Add raw HTML to your Markdown files, replacing all instances of

```
!INCLUDE "file.html"
```

With the contents of the specified file. The file can be a multi-level path.  This all happens **AFTER** the page has been generated. Super useful to avoid complications with gitbook rendering of `{% raw %} (...) {% endraw %}`

## Usage

Add to your `book.json` plugin list:
```
{
    "plugins" : [ "include-html" ],
}
```



