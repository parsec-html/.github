<p align="center">
  <img alt="Parsec: an HTML parser in Rust that reads pages the way a browser does." src="header.svg" width="100%">
</p>

<p align="center">
  <a href="https://github.com/parsec-html/parsec">Repository</a> ·
  <a href="https://github.com/parsec-html/parsec/wiki">Wiki</a> ·
  <a href="https://github.com/parsec-html/parsec/wiki/Benchmarks">Benchmarks</a> ·
  <a href="https://github.com/parsec-html/parsec/blob/main/ROADMAP.md">Roadmap</a> ·
  <a href="https://github.com/parsec-html/parsec/discussions">Discussions</a>
</p>

If you parse HTML for a living, you've probably met Lexbor, directly or through selectolax, PHP's `Dom\HTMLDocument`, nokolexbor or lazy_html. It's fast, and it follows the spec. What people keep asking it for is the rest: where a node came from in the source, XPath, selectors like `:lang()` that it parses and never matches, documents you can share across threads, and a node you still hold after it's removed that doesn't read freed memory. [Parsec](https://github.com/parsec-html/parsec) is that list, in memory-safe Rust.

```rust
use parsec::css::SelectorList;

let doc = parsec::parse("<ul><li class=hit>one<li>two</ul>", false);
let hits = SelectorList::parse("li.hit").unwrap().select(&doc, doc.root());
assert_eq!(doc.text(hits[0]), "one");
```

And it's quicker at the job. On 13 real pages, 24 MB of Wikipedia, MDN, GitHub, the BBC, the HTML spec and others, Parsec parses 370 MB a second to Lexbor's 242, ahead on every page. Throw a crawl's worst at it, 1,000 pages of broken fragments, re-encoded pages and 10 to 30 MB giants, and it gets through them in 1.02 seconds to Lexbor's 1.94, using just over half its peak memory, and nothing crashed. The [Benchmarks](https://github.com/parsec-html/parsec/wiki/Benchmarks) page has every number and how to run them yourself.

## Start here

- **[parsec](https://github.com/parsec-html/parsec)**: the parser, CSS selectors Level 4, XPath 1.0, declarative shadow DOM, the WHATWG Encoding and URL standards, and CSS stylesheets with the cascade. It passes all 7,042 html5lib tokenizer tests and every web-platform-tests tree-construction case that runs without JavaScript.
- **From Python, JavaScript or C**: bindings for each live in the same repository, free-threaded Python and WebAssembly included.
- **Install it**: 0.1.0 is out. `cargo add parsec-html`, `pip install parsec-html` or `npm install parsec-html`, and the C library is on the [release](https://github.com/parsec-html/parsec/releases/tag/v0.1.0).
- **[What's done and what's next](https://github.com/parsec-html/parsec/blob/main/ROADMAP.md)**: the line between the two is kept sharp.

## Get involved

Questions and ideas go to [Discussions](https://github.com/parsec-html/parsec/discussions). Issues labelled [good first issue](https://github.com/parsec-html/parsec/issues?q=is%3Aopen+label%3A%22good+first+issue%22) and [help wanted](https://github.com/parsec-html/parsec/issues?q=is%3Aopen+label%3A%22help+wanted%22) are a good place to start, and [CONTRIBUTING.md](https://github.com/parsec-html/parsec/blob/main/CONTRIBUTING.md) covers the rest. Found a security problem? [SECURITY.md](https://github.com/parsec-html/parsec/blob/main/SECURITY.md) says how to report it privately.
