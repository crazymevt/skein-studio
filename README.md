# Skein Studio

An IDE for [Skein](https://github.com/crazymevt/skein), written in Skein: the design of
Lisp Studio (a Common Lisp IDE) on [skein-ui](https://github.com/crazymevt/skein-ui)'s
native widgets. It edits Skein with a lexer that follows Skein's reader, and runs your
program under `skein dev`, talking to it over Swank for the REPL, debugger and inspector.

This is Skein's Phase 3 (its D-102 and D-109), built a milestone at a time; Skein's
`docs/ROADMAP.md` tracks it. Milestone M3.7 is its core: the workbench, the editor, and
running and debugging a project.

## Running it

Skein Studio uses the Skein and skein-ui checkouts beside this one:

```sh
~/projects/skein          # make compiler
~/projects/skein-ui
~/projects/skein-studio   # ./studio [folder]
```

`./studio ~/projects/my-app` opens a folder; `./studio` alone opens the last session. It
uses Cocoa on macOS (`--gtk` for GTK 4 there) and GTK 4 elsewhere. Settings and the
session are kept in the application's config directory (`Skein Studio`).

## Tests

```sh
../skein/skein test
./studio --script examples/session.edn
```

The tests run headless, and on Cocoa and GTK where those can open a window; some run a
program under a real `skein dev`. The scripted session (`examples/session.edn`, run by
`skein.studio.script`) drives the IDE as a user would: it opens `examples/sample`, runs
it, edits and evaluates, hits an error and restarts. CI runs both on macOS and Linux.

The agents' adapters are tested without Claude Code or Codex: `tools/stand-in.skn` speaks
either CLI's protocol from an EDN script (`test/agents/`), and `agents-test` builds it and
drives each adapter through a turn.
