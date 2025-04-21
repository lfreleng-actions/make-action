<!--
# SPDX-License-Identifier: Apache-2.0
# SPDX-FileCopyrightText: 2025 The Linux Foundation
-->

# 🔨 Make Action

Runs make against a given target; accepts a repository URL and/or a local
directory path as inputs.

## make-action

## Usage Example

The example below shows all combinations of inputs accepted by the action.

<!-- markdownlint-disable MD046 -->

```yaml
steps:
  - name: 'Run make'
    uses: lfreleng-actions/make-action@main
    with:
      repository: 'some-owner/some-project'
      path: '/tmp'
      makefile_path: 'resources'
      make_args: 'make install'
```

<!-- markdownlint-enable MD046 -->

## Inputs

<!-- markdownlint-disable MD013 -->

| Input Name     | Required | Description                                                  |
| -------------- | -------- | ------------------------------------------------------------ |
| repository     | False    | Remote GitHub repository to clone/download                   |
| path           | False    | Download the repository to this filesystem path              |
| makefile_path  | False    | Path to Makefile (relative to repository directory/location) |
| make_args      | False    | Arguments/flags sent to make command                         |

## Defaults

| Input Name    | Value/Behaviour                                                      |
| ------------- | -------------------------------------------------------------------- |
| repository    | Uses file in current working directory when repository not specified |
| path          | Clones repository to the current working directory                   |
| makefile_path | Uses current working directory when not provided                     |
| make_args     | Runs make without any arguments/flags                                |

<!-- markdownlint-enable MD013 -->

## Notes

This action checks for the presence of the "make" binary on the runner, but
will NOT install it if the required binary isn't found/located in the PATH.

When provided with a remote repository, the action will automatically change
into the relevant folder once it has downloaded; you do not need to specify
the downloaded repository/folder separately. Use the "makefile_path" input to
specify where the target "Makefile" is relative to the repository root
folder/location.
