#git常见问题


1. Remote rejected(shallow update not allowed)

``` bash
$ rm -rf .git // it usually is a no-no to revise or delete version history, but it's fine for my project since I don't plan on interacting with the source repo at all.
$ git init // reinitializes git
$ git remote add origin your-remote-url
$ git push -u origin master // the -u option adds an upstream tracking reference, which basically tells git where the current source of truth is (in this case, biased toward your local)

```