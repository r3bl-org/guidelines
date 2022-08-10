# R3BL code style guide
<a id="markdown-r3bl-code-style-guide" name="r3bl-code-style-guide"></a>


Table of contents

<!-- TOC -->

- [Ideals](#ideals)
  - [Favor convention over ceremony](#favor-convention-over-ceremony)
  - [Favor readability over cleverness](#favor-readability-over-cleverness)
  - [Favor readability over brevity](#favor-readability-over-brevity)
  - [Favor readability over verbosity](#favor-readability-over-verbosity)
  - [Favor well named intermediate variables over brevity](#favor-well-named-intermediate-variables-over-brevity)
  - [Favor loosely coupled and strongly coherent over tightly coupled](#favor-loosely-coupled-and-strongly-coherent-over-tightly-coupled)
  - [Favor shallow imports over deep ones by re-exporting from modules](#favor-shallow-imports-over-deep-ones-by-re-exporting-from-modules)
- [Examples](#examples)
  - [Using DSLs where appropriate](#using-dsls-where-appropriate)

<!-- /TOC -->

## Ideals
<a id="markdown-ideals" name="ideals"></a>


### 1. Favor convention over ceremony
<a id="markdown-favor-convention-over-ceremony" name="favor-convention-over-ceremony"></a>


### 2. Favor readability over cleverness
<a id="markdown-favor-readability-over-cleverness" name="favor-readability-over-cleverness"></a>


### 3. Favor readability over brevity
<a id="markdown-favor-readability-over-brevity" name="favor-readability-over-brevity"></a>


### 4. Favor readability over verbosity
<a id="markdown-favor-readability-over-verbosity" name="favor-readability-over-verbosity"></a>


### 5. Favor well named intermediate variables over brevity
<a id="markdown-favor-well-named-intermediate-variables-over-brevity" name="favor-well-named-intermediate-variables-over-brevity"></a>


### 6. Favor loosely coupled and strongly coherent over tightly coupled
<a id="markdown-favor-loosely-coupled-and-strongly-coherent-over-tightly-coupled" name="favor-loosely-coupled-and-strongly-coherent-over-tightly-coupled"></a>


### 7. Favor shallow imports over deep ones by re-exporting from modules
<a id="markdown-favor-shallow-imports-over-deep-ones-by-re-exporting-from-modules" name="favor-shallow-imports-over-deep-ones-by-re-exporting-from-modules"></a>


TK: Take some inspiration from <https://kotlinlang.org/docs/coding-conventions.html>

## Examples
<a id="markdown-examples" name="examples"></a>


### Using DSLs where appropriate
<a id="markdown-using-dsls-where-appropriate" name="using-dsls-where-appropriate"></a>


Here's an example of using a DSL to make code more readable, and respecting the following rules from
above:

- [favor readability over verbosity](#favor-readability-over-verbosity)
- [favor well named intermediate variables over brevity](#favor-well-named-intermediate-variables-over-brevity)

> What is a DSL? A DSL is a domain-specific language. Here are two good resources to learn about
> them:
>
> - <https://en.wikipedia.org/wiki/Domain-specific_language>
> - <https://docs.microsoft.com/en-us/visualstudio/modeling/how-to-define-a-domain-specific-language?view=vs-2022>

```rust
pub fn append_quit_msg_center_bottom(queue: &mut TWCommandQueue, size: Size)  {
  let message: String = "Press Ctrl + q to exit!".into();
    [
      TWCommand::MoveCursorPositionAbs(((size.cols / 2) - message.chars().count() as u16 / 2, size.rows - 1).into()),
      TWCommand::PrintWithAttributes(message, None),
    ].iter().for_each(|cmd| {
      queue.push(cmd.clone());
    });
}
```

```rust
pub fn append_quit_msg_center_bottom(queue: &mut TWCommandQueue, size: Size) {
  let message: String = "Press Ctrl + q to exit!".into();
  let col_center: UnitType = size.cols / 2 - convert_to_base_unit!(message.len()) / 2;
  let row_bottom: UnitType = size.rows - 1;
  tw_command_queue!(
  queue push
    TWCommand::MoveCursorPositionAbs((col_center,row_bottom).into()),
    TWCommand::PrintWithAttributes(message, None)
  );
}
```
