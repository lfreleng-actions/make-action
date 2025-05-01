<!--
# SPDX-License-Identifier: Apache-2.0
# SPDX-FileCopyrightText: 2025 The Linux Foundation
-->

# 🔨 Make Action

Runs "make" against a given target/Makefile, either locally or from a
downloaded/remote repository. Can optionally pass flags to the make command.

## make-action

## Usage Example

The simplest example runs make against the local directory. Without passing
any arguments, the "Makefile" must be in the current working directory:

```yaml
steps:
  - name: 'Run make'
    uses: lfreleng-actions/make-action@main
```

The next example pulls down a repository containing a Makefile to a local
folder, then runs make inside that project directory:

<!-- markdownlint-disable MD046 -->

```yaml
steps:
  - name: 'Run make'
    uses: lfreleng-actions/make-action@main
    with:
      repository: 'some-owner/some-project'
      path: 'some-project'
      make_args: '-C some-project'
```

The example below checks out the remote repository at the current directory:

```yaml
steps:
  - name: 'Run make'
    uses: lfreleng-actions/make-action@main
    with:
      repository: 'some-owner/some-project'
```

Note: this replaces any previous content in the current working directory

<!-- markdownlint-enable MD046 -->

## Inputs

<!-- markdownlint-disable MD013 -->

| Input Name | Required | Description                                     |
| ---------- | -------- | ----------------------------------------------- |
| repository | False    | Remote GitHub repository to clone/download      |
| path       | False    | Download the repository to this filesystem path |
| make_args  | False    | Arguments/flags sent to make command            |
| debug      | False    | Set true to enable diagnostic output            |

<!-- markdownlint-enable MD013 -->

## Defaults

<!-- markdownlint-disable MD013 -->

| Input Name    | Value/Behaviour                                           |
| ------------- | --------------------------------------------------------- |
| repository    | Runs make against local directory                         |
| path          | Clones remote repository to the current working directory |
| make_args     | Runs make without any arguments/flags                     |
| debug         | Debugging not enabled                                     |

<!-- markdownlint-enable MD013 -->

## Notes

This action checks for the presence of the "make" binary on the runner, but
will NOT install it if the required binary isn't found/located in the PATH.

Will automatically populate make_args with `"-C {{ inputs.path }}"` when
repository provided and path specified, but make_args is empty.
