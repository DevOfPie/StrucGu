# Setup for violates-DL-03

`DL-03` inspects git history, and a fixture cannot carry a nested repository.
Build the violating history before running a checker against this tree:

```sh
git init .
git add decisions.md strucgu.yaml
git commit -m "initial"
# now edit an entry away rather than appending a correction
sed -i '/Updating in place/d' decisions.md
git commit -am "tidy up the decision log"
```

Set `effective_from` in `strucgu.yaml` to the first commit. A correct checker
reports `DL-03` against the second commit.

**This is the one fixture that is not self-contained.** Recorded as a known gap
in the work record for the fixtures unit rather than papered over: every other
check is covered by a tree a checker can read as it stands.
