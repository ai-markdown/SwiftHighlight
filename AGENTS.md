# Contributor Guidelines

This repository is the AI Markdown fork of [CreatureSurvive/SwiftHighlight](https://github.com/CreatureSurvive/SwiftHighlight). It provides the default code syntax highlighter for the optional `AIMarkdownCodeHighlight` product of [ai-markdown-swift](https://github.com/ai-markdown/ai-markdown-swift).

## Branches and baseline

- Maintain AI Markdown changes on the `ai-markdown` branch, which is the default branch of this fork.
- Preserve the upstream `main` branch as a mirror of upstream. Never commit AI Markdown changes to it or rewrite its history.
- The `ai-markdown` branch starts from upstream release `1.0.0` (`6e405acc136ab9ee0f6584d28d73cb62a30ee246`), the version evaluated for AI Markdown. Do not combine maintenance changes with an upstream upgrade; adopting a newer upstream revision is a separate, explicitly reviewed change that must be revalidated.

## Consumption by ai-markdown-swift

- ai-markdown-swift declares this package as a remote SwiftPM dependency pinned by an exact `revision:` and records the same commit as the `Dependencies/swifthighlight` development submodule (`update = none`). Branch names never replace revision pins.
- Push commits to this fork first. Then update the parent repository's gitlink, `Package.swift` revision, `Package.resolved`, and `scripts/package-split/manifest.json` together.
- For co-development, run `bash scripts/dependencies.sh local` in ai-markdown-swift. It overrides the `swifthighlight` package with `swift package edit --path Dependencies/swifthighlight`, so uncommitted changes here are built directly. Switch back with `bash scripts/dependencies.sh remote` before committing the parent lock file.
- Only the optional `AIMarkdownCodeHighlight` target of ai-markdown-swift may depend on this package. Its Engine, Core, and UI targets must not. Keep existing product and module names stable unless the parent repository is updated in the same release sequence.

## Repository constraints

- Preserve upstream licenses, copyright notices, and meaningful source data, including multilingual fixtures.
- Language coverage does not need to match highlight.js; prioritize correctness, bounded cost on pathological input, and stable incremental (`HighlightSession`) results over adding long-tail grammars.
- Write all new or modified development text in English, including documentation, code comments, diagnostics, log messages, test descriptions, and commit messages.
- Keep the package buildable with Swift 6 language mode for iOS 26 and macOS 26 consumers, and keep ordinary builds independent of the AI Markdown workspace or external generators.
- Keep upstream tests and add regression tests for each fix. Run checks appropriate to each change, and do not present historical results as new validation.

## Commit messages

- Follow [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) using `<type>[optional scope][!]: <description>`.
- Use `feat` for new functionality, `fix` for bug fixes, and other types such as `docs`, `test`, or `refactor` as appropriate.
- Describe what the commit changes. Add a body when needed to explain the behavior or reasoning, separated from the subject by a blank line.
- Mark breaking changes with `!` after the type or scope, or with a `BREAKING CHANGE: <description>` footer.
