# Future Tasks & Hints

- **Translate Source Code**: Translate user-facing strings (CLI output, templates) in `src/**/*.ts` from Chinese to English.
  - Run `grep -r "[\u4e00-\u9fa5]" src/` to find these strings.
- Check if any new markdown files were added since the start of the task.
- Run a grep for Chinese characters to ensure nothing was missed: `grep -r "[\u4e00-\u9fa5]" .`
- Verify that links in the translated markdown files still point to the correct locations (though filenames didn't change, anchors might have if headers changed).

## Remaining Files (if any)
./plan.md
