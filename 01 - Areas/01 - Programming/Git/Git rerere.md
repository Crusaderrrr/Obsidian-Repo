**Reuse Recorded Resolution**
This is a git feature, that makes conflict resolution simpler.
It basically makes git remember/cache how the conflict for a certain file was resolved so then we can reuse this solution.

1. It needs to be enabled first `git config --global rerere.enabled true`
2. When some conflict occur and is resolved, git "remembers" the resolution
3. If same conflict happens git auto resolves it and you can review it and `git add`


