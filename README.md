# FieldCompare Action

This repository provides a GitHub action around the command-line interface of [`fieldcompare`](https://gitlab.com/dglaeser/fieldcompare)
(or see the [GitHub mirror](https://github.com/dglaeser/fieldcompare). This allows an easy integration of regression tests into your
workflows.

# Usage

Comparing two files in your workflows is as simple as this:

```yml
- name: regression-test
  uses: dglaeser/action-field-compare@v1.0
  with:
    result: "file.csv"
    reference: "reference_file.csv"
```

`fieldcompare` also supports comparing all files with matching file names in two given folders. The action automatically determines if the given
arguments for `results` and `reference` are directories and does a folder comparison in that case. `fieldcompare` also has a bunch of options
that you can pass, for instance, to set custom fuzzy tolerances, etc. This action accepts the input `cli-options` that allows you to pass all options
you would like to set as a single string. For instance, to overwrite the default relative and absolute tolerance and setting specific tolerances
to be used for all fields with the name `pressure`, you could write:

```yml
- name: regression-test
  uses: dglaeser/action-field-compare@v1.0
  with:
    result: "file.csv"
    reference: "reference_file.csv"
    cli-options: "-rtol 1e-2 -atol 1e-6 -rtol pressure:1e-5 -atol pressure:1e-5"
```
