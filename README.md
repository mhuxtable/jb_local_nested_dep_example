# jsonnet nested local dependency bug demo

This repository demonstrates a bug with the `jsonnet-bundler` tool in failing
to install nested local dependencies.

To exercise the bug, switch to `src/root_module` and run `jb install`.

## Expected outcome

Dependencies are installed to library modules `module_A` and `module_B` in the
root module.

## Actual outcome

An error is rendered to the user's screen:

```
$ jb install ../../lib/module_A
LOCAL module_A -> /Users/matt/code/jb_local_nested_dep_example/lib/module_A
jb: error: failed to install packages: downloading: symlink destination path does not exist: %w: stat /jb_local_nested_dep_example/src/module_B: no such file or directory
```

This error is exhibited with `jb` version 0.4.0 and the top of tree at time of
writing
(jsonnet-bundler/jsonnet-bundler#6bb2d1af6c8a6522cfe74e7a9cf49619d18448a1).
