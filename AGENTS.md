# Repository Guidelines

## Project Structure & Module Organization
- `SeforimApp/`: Kotlin Multiplatform app (Compose). Shared code in `src/commonMain`, desktop in `src/jvmMain`, Android in `src/androidMain`.
- `SeforimLibrary/`: composite build providing domain + persistence (`core`, `dao`, `generator`), consumed as `io.github.kdroidfilter.seforimlibrary:*`.
- Shared modules: `htmlparser/`, `icons/`, `logger/`, `navigation/`, `pagination/`, `texteffects/`, `jewel/`, `network/`.
- Codegen: `cataloggen/` generates `PrecomputedCatalog.kt` used by the app.
- Tests live next to code under `src/<target>Test/kotlin` (e.g., `SeforimApp/src/jvmTest`).

## Build, Test, and Development Commands
- `./gradlew build` — build all modules.
- `./gradlew :SeforimApp:run` — run the desktop app.
- `./gradlew :SeforimApp:hotRunJvm` / `./gradlew :SeforimApp:reload` — desktop hot reload loop.
- `./gradlew :SeforimApp:installDebug` — install Android debug build.
- `./gradlew :SeforimApp:jvmTest` (or `./gradlew test`) — run tests (desktop-only or all).
- `./gradlew :SeforimApp:lint` — run static checks.
- `SEFORIM_DB=/path/to/seforim.db ./gradlew :cataloggen:generatePrecomputedCatalog` — regenerate the precomputed catalog.

## Coding Style & Naming Conventions
- Kotlin + Compose; 4-space indentation; keep lines ~120 chars.
- Naming: `PascalCase` for types/composables, `camelCase` for functions/properties, `UPPER_SNAKE_CASE` for constants.
- UI: prefer `SomethingView` and `SomethingViewModel` naming patterns.
- Keep shared logic in `commonMain`; avoid leaking platform-specific types across source sets.
- DI uses Metro (`AppGraph`, `@Provides`); access via `LocalAppGraph` (avoid singletons).

## Localization & Resources
- Never hardcode user-visible text; add keys to `SeforimApp/src/commonMain/composeResources/strings.xml`.
- The required locale for user-facing text is Hebrew (`he`); provide Hebrew strings for all new keys.

## Testing Guidelines
- Use Kotlin Test (and Compose UI testing where applicable); keep tests small and focused.
- Naming: mirror the source name with `...Test.kt` (e.g., `BookContentViewModelTest.kt`).

## Commit & Pull Request Guidelines
- Git history favors imperative subjects (often `Refactor: ...`, `Add ...`, `Fix ...`); keep the first line scannable.
- PRs should include: what changed, modules touched, linked issues, screenshots/GIFs for UI changes, and verification steps (e.g., `:SeforimApp:run`).

## Security & Configuration Tips
- Do not commit secrets or API keys; keep machine-specific settings in `local.properties`.

## Living Project Board

`PROJECT_BOARD.md` is this repository's shared living project board. Before starting substantial work, scan it for relevant context. During normal work, agents should proactively add concise, actionable entries when they discover something with genuine future value, including:

- useful technical discoveries
- optimization opportunities
- implementation tricks
- architectural ideas
- possible future improvements
- experiments worth running
- unresolved issues or questions
- follow-up work that should not be lost

Do this proactively even when the discovery is incidental to the current task. Do not add trivial observations, temporary debugging chatter, information already documented elsewhere, generic suggestions with no project relevance, or every step performed during a task. The board supports memory but is not a source of truth when repository code, documentation, or current state contradicts it.

When an item is implemented, mark it complete and optionally record the date and commit/PR, moving it to `Done` when useful. Delete or archive obsolete entries when appropriate.

Updating `PROJECT_BOARD.md` as a side effect of another task is allowed and encouraged when a worthwhile discovery is made. Recording an idea is allowed; implementing unrelated ideas is not.

Preserve all existing repository-specific instructions.
