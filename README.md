# A sample automerge-tracked collaborative paper

This repository demonstrates how to collaboratively edit a paper while tracking changes in automerge.

You will need two components: the [Automerge Tracker VSCode extension](https://github.com/pvh/vscode-automerge-tracker) to record your changes, and the [Automerge git-merge-driver](https://github.com/pvh/vscode-automerge-tracker) to reconcile the binary .mrg files. Both are extremely fragile prototypes, so expect things to go wrong!

# VSCode extension

Install this extension: https://marketplace.visualstudio.com/items?itemName=inkandswitch.vscode-automerge-tracker

We've already done it for paper.md, but run "Begin sync to an Automerge document" in the command palette on a **SAVED DOCUMENT**. You should see the .mrg file once you save that document again.

# Git merge driver

Because... reasons... you'll need to configure the git merge driver manually. The repo containing it is already included as a git submodule on this repo for your convenience.

```
$ git submodule init
$ git submodule update
$ cd automerge-git-merge-driver
$ yarn
$ cd ..
$ git config --local merge.automerge-driver.driver "node automerge-git-merge-driver/merge-automerge.js %A %B"
```

After running these commands, you should automatically merge conflicting edits to the .mrg document using the driver described above.

# Testing

* Open paper.md in your newly extended VSCode. Make some edits. Save.
* `paper.md.mrg` should have changed.
* Commit the changes.
* `git checkout -b test-branch`
* Make & save a change to the document.
* Commit both files.
* `git checkout main`
* Make & save a change to the document (you should see the pre-test-branch document when you do this.)
* Commit both files.
* Now you have a binary file conflict brewing when you merge `test-branch` back into main.
* `git merge test-branch`
* Notice that the .mrg file merged automatically by running the git-merge driver you configured above.

# BUGS

I'm sure there are loads. This is a fragile prototype. Please report them somewhere, or better yet, fix them.

What happens if both branches edit the same line? The automerge should be fine but it will probably lose consistency with the text in git.