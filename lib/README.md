<p align="center">
  <a href="https://github.com/fish-shell/wahoo/blob/master/README.md">
  <img width="100px" src="https://cloud.githubusercontent.com/assets/8317250/9700591/4f7bcd0c-5443-11e5-84cf-f5f01fa8faa6.png">
  </a>
</p>

# Core Library

## Basic Functions

#### `autoload` _`<path [path...]>`_
Autoload a function or completion path. Add the specified list of directories to `$fish_function_path`.

Any `completions` directories are correctly added to the `$fish_complete_path`.

```fish
autoload $mypath $mypath/completions
```

#### `available` _`<name>`_

Check if a program is available to run. Sets `$status` to `0` if the program is available.

Use this function to check if a plugin is available before using it:

```fish
if available battery
  battery
end
```

#### `basename` _`<path> ...`_

Wrap basename so it can handle multiple arguments.

#### `refresh`

Extract the root (top-most parent directory), dirname and basename from [`fish_prompt`](http://fishshell.com/docs/current/faq.html#faq-prompt).


#### `prompt_segments`

Replace the running instance of fishshell with a new one causing Wahoo to reload as well.


## Git Functions
#### `git_ahead`

Echo a character that represents whether the current repo is ahead, behind or has diverged from its upstream.

##### Default values:

+ ahead: `+`
+ behind: `-`
+ diverged: `±`
+ none: ` `

#### `git_is_repo`
Set `$status` to `0` if the current working directory belongs to a git repo.

#### `git_branch_name`
Echo the currently checked out branch name of the current repo.

#### `git_is_dirty`
Set `$status` to `0` if there are any changes to files already being tracked in the repo.

#### `git_is_staged`
Set `$status` to `0` if there [staged](http://programmers.stackexchange.com/questions/119782/what-does-stage-mean-in-git) changes.

#### `git_is_stashed`
Set `$status` to `0` if there are items in the [stash](https://git-scm.com/book/en/v1/Git-Tools-Stashing).

#### `git_is_touched`

Set `$status` to `0` if the repo has any changes whatsoever, including [tracked or untracked](http://stackoverflow.com/questions/9663507/what-is-tracked-files-and-untracked-files-in-the-context-of-git) files.

#### `git_untracked`
Echo a `\n` separated list of untracked files.
