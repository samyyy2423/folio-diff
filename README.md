# diff

What changed between two texts, for [Folio](https://github.com/samyyy2423/folio) programs: line by line, as
`diff -u` and git write it, or word by word, with the fewest changes (Myers' algorithm), and a diff applied to
a text again. In Folio alone, so it works everywhere Folio does.

```text
folio add diff
```

```
use the package "diff" as diff

set before to "one\ntwo\nthree\n"
set after to "one\n2\nthree\nfour\n"
say diff's unified(before, after, "a/numbers.txt", "b/numbers.txt")
say diff's marked("the quick brown fox", "the slow brown cat")
```

```text
--- a/numbers.txt
+++ b/numbers.txt
@@ -1,3 +1,4 @@
 one
-two
+2
 three
+four

the [-quick-]{+slow+} brown [-fox-]{+cat+}
```

## What it has

| | |
|---|---|
| `changes(a, b)` | a record for each line: its `op` (`"same"`, `"removed"` or `"added"`), its `words`, and `old` and `new`, its line's number in a and in b (`nothing` for a line that isn't in one) |
| `unified(a, b, old_name, new_name, context)` | the changes as `diff -u` writes them, with `context` lines (3 if none is given) around each change; `""` when nothing changed |
| `stats(a, b)` | a record of how many lines were `added` and `removed` |
| `word_changes(a, b)` | changes between words, and the spaces between them |
| `marked(a, b)` | the two texts in one line, as `git diff --word-diff` writes them: `[-removed-]{+added+}` |
| `apply(words, patch)` | the text with a unified diff's changes made: each part's lines are found near where it says they are, and it fails if they aren't there |

`a` and `b` are texts, cut at their new lines, or lists of lines. A text with no new line at its end gets
`\ No newline at end of file`, as diff writes it. `unified`'s output is GNU diff's, byte for byte (but for
the dates diff puts on its `---` and `+++` lines), and `git apply` and `patch` take it.

Past 4000 changes between two texts, `changes` stops looking for the fewest, and has the rest of the first
removed and the rest of the second added.

## Tests

```text
folio test diff.test.folio
```

## License

Apache License 2.0, as Folio is: see [LICENSE](LICENSE).
