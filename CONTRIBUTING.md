# Contributing

This repository holds the written documentation for the whole network. Contributions are welcome, including your first one.

## Ways to help that are not code

- Follow a guide, and open an issue anywhere it was confusing or wrong.
- Report a bug with the exact commands you ran and what you saw.
- Improve the docs. Fixing one unclear paragraph is a real contribution.
- Answer someone else's question in the issue tracker.

## Setting up


        Documentation is plain Markdown. No build step — open a file and edit it.

        ```bash
        git clone https://github.com/inazuma-network/inazuma-docs.git
        ```


## Workflow

1. Open an issue first for anything non-trivial, so nobody duplicates your work.
2. Fork, then branch: `fix/rpc-timeout` or `feat/batch-submit`.
3. Make one logical change per pull request. Small reviews get merged fast.
4. Write commit messages as `area: what changed` — for example `mempool: cap per-account queue`.
5. Fill in the pull request template, including how you tested it.
6. A maintainer reviews. Expect questions; they are not criticism of you.


        ## Writing rules

        - Write for someone who has never run a node. Explain a term the first time you
          use it, or link the glossary.
        - Every command must be copy-pasteable and actually work. Run it before you
          submit it.
        - Prefer a table over a wall of prose. Prefer a real example over a description.
        - No marketing language, no comparisons to other chains, no price talk.


## Reporting security bugs

Do not open a public issue. Follow [SECURITY.md](SECURITY.md).

## License

By contributing you agree your work is released under the MIT license in
[LICENSE](LICENSE).
