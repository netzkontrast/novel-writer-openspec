# Task Tracking: Translate all MD files to English

This `AGENTS.md` file is used to track the progress of translating all Markdown files in the repository from Chinese to English.

## Workflow

1.  **Pick a file** from `todo.md`.
2.  **Translate** the file content to English in-place.
3.  **Remove** the file name from `todo.md`.
4.  **Verify** the translation.

## Task List

The list of files to translate is maintained in `todo.md`.

## Updated Workflow & Best Practices

### Workflow Improvements

1.  **Batch Processing**: Instead of strictly one-by-one, grouping small files can save context switching time.
2.  **Context Awareness**: Read `project.md` and `AGENTS.md` first to understand the domain terminology before translating specific specs or changes.
3.  **Verification**: Always run `novelspec validate` (if available) or check markdown rendering to ensure no formatting was broken during translation.
4.  **Consistency**: Maintain a glossary of terms (e.g., "Specs" = 规格, "Proposal" = 提案, "Clarification" = 澄清) to ensure consistent translation across files.

### Best Practices

-   **Preserve Formatting**: Markdown headers, lists, code blocks, and bolding must remain exactly as is.
-   **Technical Terms**: Do not translate technical terms like `specs/`, `changes/`, `novelspec`, `OpenSpec` unless they are being explained.
-   **Tone**: Keep the professional and structured tone of the original documentation.
-   **Incremental Updates**: Update `todo.md` frequently to avoid double work or losing track.

## Continuous Improvement

-   **Reflect**: After each major section (e.g., all `openspec/` files), review if terminology is consistent.
-   **Automate**: If doing this again, a script to grep for untranslated Chinese characters could be useful to spot missed sections.
-   **Feedback Loop**: If a file was hard to translate due to ambiguity, mark it for clarification in the translation notes.

## Reflection on this Task

-   **Process**: The process of listing files in `todo.md` and removing them one by one worked well to keep track of progress.
-   **Challenge**: Some files contained mixed Chinese and English (code vs comments). Care was needed to only translate comments and prose, not code logic or variable names.
-   **Improvement**: Future tasks could benefit from a pre-scan of terminology to build a glossary upfront.

