# `steps`
Manage steps for demo projects using git tags

## Installation

Download the steps shell file and put it somewhere in your path. If you want, you can do this in a one-liner:

```bash
sudo wget https://raw.githubusercontent.com/superMDguy/steps/HEAD/steps -O /usr/local/bin/steps && sudo chmod +x /usr/local/bin/steps
```

## Example usage

1. Get the repository to an intial state, which will be the starting point of your demo. This could be an empty directory, or it could be some boilerplate. Whatever it is, make sure you've initialized a git repository, and added at least one commit.

```bash
mkdir my-project
cd my-project
git init
echo "Hello, World" >> code.py
git commit -am "initial commit"
```

2. Add the first step. This will add a tag to the most recent commit with the name of your step.

```
steps add init # or step_1, or anything you want, as long as it doesn't have spaces (even quoted ones).
```

3. Add the rest of your steps. You can have as many commits in between steps as you want, just make sure you commit before you run `steps add`.

4. At some point, you'll probably want to change a past step. Here's where `steps` is really useful. To start out, run `steps workon` to create a temporary branch that you can use to make changes to a past step.

```bash
steps workon init
```

Next, you can make as many commits as you want on this branch. When you're done, run `steps update`. This will update the tag for the step, and run a rebase command that will insert your commits on top of the step you're working on. You'll probably have conflicts. When you do, resolve them, and run `git rebase --continue`. Once all your conflicts are resolved, run `steps sync` to resync the tags with the commits (rebasing changes commit hashes, which removes tags).

5. During the demo, you can go to different steps by running `steps view <step_name>`. You can make any changes you want, but you'll be in a detached head so they won't be permanent. So, you can livecode examples, then skip to the next step.

## Other Commands

* `steps remove <step_name>`
* `steps diff <step_name>` shows diff between current head and the given step
* `steps list`
