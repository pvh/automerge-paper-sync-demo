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

# BUGS

I'm sure there are loads. This is a fragile prototype. Please report them somewhere, or better yet, fix them.
