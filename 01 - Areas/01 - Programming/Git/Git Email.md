Git can export commit diffs as files and also send them via SMTP.

**The two core commands are**:
**`git format-patch`** — exports one or more commits as `.patch` files. Each file contains the diff plus metadata (author, commit message, timestamp). These are plain text, so you can literally email them.

**`git am`** (apply mailbox) — receives those patch files and applies them as proper commits, preserving the original author and message.

```bash
# Sender: export last 3 commits as patch files
git format-patch HEAD~3

# Receiver: apply the patch
git am 0001-fix-login-bug.patch
```

There's also `git send-email`, a higher-level command that actually sends the patches via SMTP directly from your terminal — this is how the Linux kernel workflow operates to this day.

*This is almost never used in practice, but it is interesting to know =)*