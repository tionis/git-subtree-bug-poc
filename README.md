# subtree bug proof of concept
this is a test repo to test a possible bug in git-subtree

When a subtree was added, removed and later added again it leads to errors when pushing new commits in the subtree, as the split fails due to some caching error.
This command:
```bash
git subtree split --prefix embedded-repo
```
will fail with the following error message:
```
fatal: cache for 2e518bdc769cb08f51bb9869c7100439d76849a6 already exists!
```
Here's a more verbose output:
```bash
$ git subtree split --prefix embedded-repo/ --debug
command: {split}
quiet: {}
dir: {embedded-repo}
opts: {}

Splitting embedded-repo...
Using cachedir: /home/tionis/subtree-test/.git/subtree-cache/34770
Looking for prior splits...
  Main is: 'b20c739a0d725295863ba2d3bfc20c6e672a1d06'
    Prior: b20c739a0d725295863ba2d3bfc20c6e672a1d06 -> 2e518bdc769cb08f51bb9869c7100439d76849a6
  Main is: 'df13f9517d20c4a694a02f8641ee053ea2ff608d'
    Prior: df13f9517d20c4a694a02f8641ee053ea2ff608d -> 2e518bdc769cb08f51bb9869c7100439d76849a6
fatal: cache for 2e518bdc769cb08f51bb9869c7100439d76849a6 already exists!
```
