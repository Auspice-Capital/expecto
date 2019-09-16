# Devguide

2 space indentation, please.

## Setup

 1. **EditorConfig** – If you haven't already, install the EditorConfig
    extension to prevent any conflicts between your default F# formatting
    conventions and the ones used by this project.
    * Visual Studio - [EditorConfig VS Extension][ec-vs]
    * VS Code - [EditorConfig VScode Extension][ec-vsc]

 1. You will need .NET Core [v2.1 SDK][netcore-sdk] installed. The versions of Mono and .NET Core currently tested in CI can be found [here in .travis.yml][travis]

 1. Ensure .Net Core tools are on your PATH: `$HOME/.dotnet/tools`

 1. Set up of compiler state:

    ```bash
    source .env
    ./fake build
    ```

 1. New features:
      * Make your test for your change
      * Make your change
      * If appropriate, write docs in README.md.

## Code style

 1. For variables: prefer `test` over `t`. Prefer `test` over
    `sequencedTestCode`.
 1. Try to stick to max 80 chars wide lines, unless it improves readability to
    let the line be longer. `set tw=80` can be used in vim.
 1. If you have a function that takes a list of tests, `let run` then it's
    better to name the list/seq `ts` than `l` for three reasons:
      1. You may be using a sequence an not a list in the future, so `l` is not
         necessarily forwards-compatible.
      2. When iterating `ts`, it becomes natural to read and understand each
         element as `t`: `Seq.mapi (fun i t -> ...)`
      3. `l` is easily confused with `I` and `1`, depending on typeface.

Futhermore, in no particular order;

 - Spaces after function names.
 - Spaces after parameter names like so `param : typ`.
 - 2 space indentation.
 - Use `lowerCaseCamelCase`, also on properties.
 - Interfaces *do not* start with `I`. Can you use a function instead, perhaps?
 - LF (not CRLF) in source files.
 - Prefer flat namespaces.
 - Prefer namespaces containing *only* what a consumer needs to use – no
   utilities should be public if it can be helped.
 - Follow the existing style of the library.
 - For single-argument function calls, prefer `fn par` over `par |> fn`. For
   multiple-argument function calls, `par3 |> fn par1 par2` is OK.
 - No final newline in files, please.
 - Open specify `open` directives for the used namespaces and modules.
 - Prefer to cluster `open` directives at the top of the file.
 - Remember to follow [the guidelines!](http://devopsreactions.tumblr.com/post/140324458371/when-someone-doesnt-follow-the-coding-style)

## Invariants

 - I will release this project if all tests go through. If you contribute
   functionality you need to make sure that all tests pass and that the intended
   functionality is properly tested, otherwise it may break at any time.
 - Prefer to test all cases of your code, over testing only the happy path.

## Logging/printing from within Expecto

 - If you want the logging/printing to properly print before the process exists,
   you need to use the `logWithAck` function, because the returned async will
   yield when the data has been written to the configured output.

## Releasing

`fake build -- --target Release`

[ec-vs]: https://marketplace.visualstudio.com/items?itemName=EditorConfigTeam.EditorConfig
[ec-vsc]: https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig
[netcore-sdk]: https://www.microsoft.com/net/download
[netcore-rt]: https://github.com/dotnet/core/blob/master/release-notes/download-archive.md#net-core-11
[travis]: https://github.com/haf/expecto/blob/master/.travis.yml
[mono-dl]: http://www.mono-project.com/download/
[fake]: https://fake.build/fake-gettingstarted.html

