# SwiftUI Markdown

SwiftUI `Markdown` is a Swift package for render markdown text in SwiftUI. Use just like SwifUI Text.

## Usage

```swift
import Markdown

var body: some View {
  Markdown("You can try **MarkdownKit** [here](https://github.com/bmoliveira/MarkdownKit).")
}
```

## Supported Elements

```
*italic* or _italics_
**bold** or __bold__
~~strikethrough~~

# Header 1
## Header 2
### Header 3
#### Header 4
##### Header 5
###### Header 6

> Quote

* List
- List
+ List

`code` or ```code```
[Links](https://github.com/viere1234/SwiftUI-Markdown)
```

## Extensibility

To add new Markdown elements all you have to do is implement the `MarkdownElement` protocol (or descendants) and add it to the `Markdown`.

```swift
import Markdown

class MarkdownSubreddit: MarkdownLink {

  private static let regex = "(^|\\s|\\W)(/?r/(\\w+)/?)"
  
  override var regex: String {
    return MarkdownSubreddit.regex
  }
  
  override func match(
    match: NSTextCheckingResult,
    attributedString: NSMutableAttributedString
  ) {
    let subredditName = attributedString.attributedSubstringFromRange(match.rangeAtIndex(3)).string
    let linkURLString = "http://reddit.com/r/\(subredditName)"
    formatText(attributedString, range: match.range, link: linkURLString)
    addAttributes(attributedString, range: match.range, link: linkURLString)
  }
}
```
