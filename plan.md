
1. *Setup and Discovery*
   - List all markdown files in the repository.
   - Create `todo.md` in the root directory listing all markdown files to be translated.
   - Add `AGENTS.md` to the root (or update the existing one) to track the task and explain the workflow.

2. *Translate Root Files*
   - Translate `README.md` from Chinese to English.
   - Translate `AGENTS.md` (root) from Chinese to English, while also ensuring it includes the task tracking information.
   - Remove these files from `todo.md`.

3. *Translate `novelspec` and `openspec` Files*
   - Iterate through the remaining files in `todo.md`.
   - For each file:
     - Read the content.
     - Translate it to English in-place.
     - Update `todo.md` by removing the file.
     - *Self-Correction/Verification*: Check if the translation is reasonable and format is preserved.

4. *Continuous Improvement & Reflection*
   - Before the final commit, reflect on the process.
   - Update `AGENTS.md` with "Best Practices" and an "Updated Workflow" based on the experience.
   - Ensure `AGENTS.md` includes steps for continuous improvement for future tasks.
   - Add hints to the top of `todo.md` (if any items remain or for future usage) or a new `NEXT_STEPS.md` if `todo.md` is empty/deleted (Plan says "give Additional hints on what to do Next - at the start of the todo.md"). I will likely keep `todo.md` but empty or with future tasks if any. Actually, the user says "remove the corresponding filename from the List", so eventually it should be empty. But then says "give Additional hints... at the start of the todo.md". So I will keep the file with hints.

5. *Pre-commit & Submit*
   - Run pre-commit checks.
   - Submit the changes.
