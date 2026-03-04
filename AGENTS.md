# Repository Guidelines

## Project Structure & Module Organization
This repository is centered on the Kotlin Multiplatform SDK in [`sdk/`](./sdk).
- `sdk/library`: main published SDK module (`commonMain`, `androidMain`, `iosMain`, `linuxX64Main` + platform tests).
- `sdk/krux`: secondary KMP module with Android/iOS targets and host/device tests.
- `sdk/buildSrc`: shared Gradle convention/plugin code used by modules.
- `docs/`: documentation workspace (currently minimal).

Keep shared business logic in `commonMain`; use platform source sets only for platform-specific APIs.

## Build, Test, and Development Commands
Run commands from `sdk/`.
- `./gradlew build`: compile all modules and run configured checks.
- `./gradlew check`: run verification tasks (including lint/test where configured).
- `./gradlew :library:build`: build only the main SDK module.
- `./gradlew :krux:build`: build only the `krux` module.
- `./gradlew :library:publishToMavenLocal`: publish artifacts locally for integration testing.
- `./gradlew :library:publishToMavenCentral`: publish release artifacts (requires signing and Maven credentials).

Tip: use `./gradlew tasks --all` to inspect target-specific tasks on your machine.

## Coding Style & Naming Conventions
- Kotlin style is `official` (`sdk/gradle.properties`); follow idiomatic Kotlin and keep files focused.
- Use 4-space indentation, PascalCase for types, camelCase for functions/properties, and lowercase package names (`com.micrantha.bluebell...`).
- Match source-set naming conventions (`commonMain`, `androidMain`, `iosTest`, etc.).
- Prefer small, composable modules and unidirectional data flow patterns already used in `library`.

## Testing Guidelines
- Primary framework: `kotlin.test`; Android instrumentation uses `androidx.test`.
- Place tests in matching source sets (`commonTest`, `jvmTest`, `linuxX64Test`, `androidHostTest`, `androidDeviceTest`).
- Name test files with `*Test.kt` and use descriptive test names (backticked names are acceptable).
- Run `./gradlew check` before opening a PR.

## Commit & Pull Request Guidelines
- Follow concise, imperative commit subjects. Prefer Conventional Commit prefixes (`feat:`, `fix:`, `docs:`), consistent with existing history.
- Keep commits scoped to one logical change.
- PRs should include: summary, affected modules, verification steps/commands run, and linked issue(s) if applicable.
- For UI/API behavior changes, include screenshots or sample usage snippets.

## Security & Release Notes
- Never commit secrets, signing keys, or Maven Central credentials.
- Keep publishing configuration changes in `sdk/library/build.gradle.kts` and document release-impacting updates in the PR.
