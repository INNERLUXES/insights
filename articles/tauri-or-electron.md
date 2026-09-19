# Tauri or Electron: what we check before we recommend Tauri

Canonical version: https://innerluxes.dev/browser-development/tauri

Tauri is the right choice for many desktop apps and the wrong one for some. Before we quote, we check the product
against the points below, and we tell you if the answer is Electron or a native app.

## Who is going to maintain the Rust side

A Tauri app has a Rust core. If your team is all web developers, someone has to own that core after handover. We write
it in plain, documented Rust, keep the commands the front end calls small and typed, and hand over a short guide to
the layout. If nobody on your side wants to touch Rust, we say so before you commit.

## WebView differences between operating systems

Tauri uses the WebView that ships with each operating system, so the same page can behave differently on Windows,
macOS and Linux. We test on all three from the first build, and we avoid features that only one WebView supports
unless you tell us the app targets a single platform.

## Tauri Electron migration

Moving an existing Electron app to Tauri is a rewrite of the native layer, not the interface. The front end usually
carries over. Node.js code that touched the file system, the tray or the updater has to move into Rust commands. We
list every Electron API the app uses, decide what each one becomes, and agree the scope before any code is written.

## Signed installers and auto-update

A desktop app is not finished until a user on a locked-down machine can install it and receive the next release
without help. We set up code signing, notarization on macOS, signed update manifests and a rollback path in the first
weeks, because leaving them to the end is how launches slip.

## Security of the bridge between page and Rust

Tauri lets the page call Rust commands, and the list of commands the page can call is a security boundary. We expose
only what the screen needs, give each command narrow permissions, and review the capability configuration with you
before release.

## When we would choose something else

If the app depends on a specific Chromium feature, needs a browser engine that behaves identically on every machine,
or is a browser in its own right, Electron or a Chromium-based build is the better fit. We build those too, see
[Chromium development](https://innerluxes.dev/browser-development/chromium).

---

Related on innerluxes.dev: [Tauri desktop app development](https://innerluxes.dev/browser-development/tauri), [Chromium development](https://innerluxes.dev/browser-development/chromium).
