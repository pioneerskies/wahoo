<div align="center">
  <a href="http://github.com/fish-shell/wahoo">
    <img width=120px  src="https://cloud.githubusercontent.com/assets/8317250/9700591/4f7bcd0c-5443-11e5-84cf-f5f01fa8faa6.png">
  </a>
</div>

<br>

<p align="center">
<b><a href="#issues">Issues</a></b>
|
<b><a href="#package-repositories">Packages</a></b>
|
<b><a href="#commit-messages">Commit Messages</a></b>
|
<b><a href="#code-style">Code Style</a></b>
</p>

# Contributing

Thanks for taking the time to read this guide and please _do_ contribute to Wahoo. This is an open initiative and _everyone_ is welcome. :metal:

## Issues

Please [open an issue](https://github.com/fish-shell/wahoo/issues) for bug reports / patches. Include your OS version, code examples, stack traces and everything you can to help you debug your problem.

If you have a new feature or large change in mind, please open a new issue with your suggestion to discuss the idea together.

You are also welcome to our [Gitter room](https://gitter.im/fish-shell/wahoo).

## Package Repositories

This is the repository for the core Wahoo framework and bootstrap installer.

If your issue is related to a specific package, we still may be able to help, but consider visiting that package's issue tracker first.

## Commit Messages

+ Use the [present tense](https://simple.wikipedia.org/wiki/Present_tense) ("add awesome-package" not "added ...")

+ Less than 72 characters or less for the first line of your commit.

+ Use of [emoji](http://www.emoji-cheat-sheet.com/) is definitely encouraged. :lollipop:

## Code Style

> These rules are not set in stone. Feel free to open an issue with suggestions and/or feedback.

### Control Flow

Using `if..else..end` blocks is preferred.

```fish
if not set -q ENV_VARIABLE
  set -g ENV_VARIABLE 42
end
```

The following syntax is more concise, but arguably less transparent.

> You still may use `and` / `or` statements if you consider `if..else..then` to be overkill.

```fish
set -q VAR; set -g VAR 42
```

### Functions

Use named arguments `-a`:

```fish
function greet -a message
  echo "$message"
end
```

Use `-d` description fields:

```fish
function greet -a message -d "Display a greeting message"
  echo "$message"
end
```

`fish` does not have private functions, so in order to avoid polluting the global namespace, use a prefix based in the scope of your code. For example, if you are writing a `ninja` plugin using `__ninja_function_name`.

If you are writing a function inside another function, prefix the inner one with the parent's name.

```fish
function parent
  function parent_child
  end
end
```

Note that it's still possible to mimic private functions in `fish` by deleting the function before returning using `functions -e function_name`

```fish
function public_func
  function private_func
    # ...
    functions -e private_func
  end
end
```

### Blocks

Blocks allow you to write code resembling macro expressions composed of smaller blocks without relying on variables.

Compare the following _without_ blocks:

```fish
set -l colors green1 green2 green3
if test $error -ne 0
  set colors red1 red2 red3
end

for color in $colors
  printf "%s"(set_color $color)">"
end
```

and _using_ blocks:

```fish
for color in (begin
  if test $error -ne 0
    and printf "%s\n" red1 red2 red3
    or printf "%s\n" green1 green2 green3
  end)
  printf "%s"(set_color $color)">"
end
```

The second example does not use a `colors` variable.

:heart:
