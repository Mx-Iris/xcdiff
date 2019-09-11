# xcdiff

A tool to help diff your .xcodeproj files

## Development

### SwiftLint

We've set up SwiftLint (https://github.com/realm/SwiftLint) to enforce Swift style and conventions.
You can run the following command to check if your code does not violate any of the rules.

```
swiftlint
```

### SwiftFormat

We've set up SwiftFormat (https://github.com/nicklockwood/SwiftFormat) to enforce consistent code formatting.

You can run the following command to format your code.

```
swiftformat .
```

### Command Tests

All markdown files in `CommandTests/Manual` were created manually, `CommandTests/Generated` contains test files that are auto-generated by the script `Scripts/generate_tests_commands_files.py`. Thanks to those tests, there is no need to write any new manual tests. We need to just focus on reviewing the new markdown files generated in `CommandTests/Generated` to make sure the files contain the expected output of your new comparator. Scan the file names in `CommandTests/Generated` for your new dependency tag name or check `git status` for new markdown files if you have trouble finding the newly generated files by the script.

**IMPORTANT:** To add a new comparator add the comparator's tag to `Scripts/generate_tests_commands_files.py` and run the script to generate the tests. The script needs to be updated and run every time we add a new comparator.

Each markdown file in `CommandTests` represents a single integration test. Those files follow a very specific pattern:

```
    # Command
    ```json
    <JSON REPRESENTATION OF THE COMMAND>
    ```

    # Expected exit code
    <NUMBER>

    # Expected output
    ```
    <CONTENT OF THE OUTPUT>
    ```
```

i.e.

```
    # Command
    ```json
    ["-p1", "{ios_project_1}", "-p2", "{ios_project_2}"]
    ```

    # Expected exit code
    1

    # Expected output
    ```
    ❌ TARGETS > NATIVE targets
    ❌ TARGETS > AGGREGATE targets
    ❌ SOURCES > "Project" target
    ❌ SOURCES > "ProjectTests" target
    ❌ SOURCES > "ProjectUITests" target
    ❌ RESOURCES > "Project" target
    ❌ RESOURCES > "ProjectTests" target
    ❌ RESOURCES > "ProjectUITests" target


    ```
```

`generate_tests_commands_files.py` helps to generate the most obvious cases, like different permutations of the verbose or format options.

## Code of Conduct

This project has adopted a
[Code of Conduct](https://github.com/bloomberg/.github/blob/master/CODE_OF_CONDUCT.md).
If you have any concerns about the Code, or behavior which you have experienced
in the project, please contact us at opensource@bloomberg.net.

## Security Vulnerability Reporting

If you believe you have identified a security vulnerability in this project,
please send email to the project team at opensource@bloomberg.net, detailing
the suspected issue and any methods you've found to reproduce it.

Please do NOT open an issue in the GitHub repository, as we'd prefer to keep
vulnerability reports private until we've had an opportunity to review and
address them.

## License

xcdiff is released under version 2.0 of the [Apache License](License.txt).
