Commit all current changes to git with a concise commit message.

1. Run `git status` and `git diff` to see all changes
2. Stage all changes with `git add -A`
3. Create a commit with a very concise title (max 50 chars) and brief description
4. Format:
   ```
   <type>: <short summary>

   <1-2 sentence description of what changed>

   🤖 Generated with [Claude Code](https://claude.com/claude-code)

   Co-Authored-By: Claude <noreply@anthropic.com>
   ```
5. Use conventional commit types: feat, fix, docs, chore, refactor
