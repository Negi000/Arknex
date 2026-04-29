# Arknex

Language: [English](#arknex) | [日本語](#arknex-日本語)

Arknex is a Unity and Unreal asset workbench for fast browsing, indexing, searching, previewing, and plugin-driven asset workflows.

This repository is a release-only public handoff for Arknex 1.0.0.0 (win-x64). It contains the public README, checksum information, and the source-free Windows runtime package or release asset reference. The development source tree is intentionally not part of this repository.

## What Arknex is

Arknex is a desktop workbench for teams and individual developers who need to inspect and organize assets from Unity and Unreal projects. It is designed to make existing asset libraries easier to browse, search, preview, compare, and reuse without turning the application core into a collection of project-specific hacks.

At its core, Arknex combines three ideas:

1. A practical viewer for Unity and Unreal asset sources.
2. A searchable index and asset workspace for large project folders.
3. An SDK-first plugin platform that lets developers build their own workflows on top of Arknex instead of modifying the core application.

## Main features

- Unity and Unreal support in one desktop workbench.
- Project registration, source scanning, and asset indexing.
- Asset list, search, filtering, and detail inspection.
- Preview routing for supported asset types and graceful diagnostics for unsupported files.
- Export-oriented workflow foundations for future automation and reuse.
- Plugin Diagnostics for trust level, capabilities, contribution points, commands, actions, and load failures.
- Arknex Data Intelligence as a first-party flagship plugin prototype and SDK compatibility probe.
- Source-free release packaging with checksum and manifest validation.

## SDK-first extensibility

Arknex is intentionally built around Arknex.SDK and a microkernel-style Host boundary. The goal is unlimited practical extensibility: personal developers should be able to create custom viewers, dashboards, reports, validators, exporters, data workspaces, and project-specific helpers as plugins.

Current public extension seams include:

- typed active project context;
- plugin workspace descriptors;
- structured action results;
- command and action diagnostics;
- read-only Host-indexed source access;
- capability and trust metadata;
- descriptor-driven UI sections for plugin workspaces.

The core rule is simple: common platform behavior belongs in Arknex, while project-specific workflows should live in plugins.

## Download and integrity

Runtime package: Arknex-1.0.0.0-win-x64.zip

Checksum sidecar: Arknex-1.0.0.0-win-x64.zip.sha256

Expected SHA256: 731af77974b64b843f1a7a36e9003db308cfc8da1ac6de86ae7306d88abd53ec

Before first launch, verify the ZIP hash with PowerShell:

    Get-FileHash -Algorithm SHA256 .\Arknex-1.0.0.0-win-x64.zip
    Get-Content .\Arknex-1.0.0.0-win-x64.zip.sha256

If the hash does not match, delete the ZIP and download it again.

Important GitHub note: the generated ZIP can be larger than GitHub's normal 100 MiB per-file repository limit. When that applies, track the ZIP with Git LFS or keep the README and checksum in the repository and attach the ZIP to GitHub Releases instead of committing the ZIP as a normal repository file.

## Quick start

1. Download the Windows x64 runtime ZIP.
2. Verify the SHA256 checksum.
3. Extract the ZIP to a writable folder.
4. Keep Arknex.exe and the _arknex folder together.
5. Run Arknex.exe.
6. Use Plugin Diagnostics if a bundled or external plugin does not load.

Do not distribute a locally smoke-tested dist folder. Local runs can create settings, logs, cache, and database files that are intentionally excluded from the public release package.

## Release contents

The runtime ZIP is generated from an allowlisted staging layout and is validated before publication. It contains runtime files such as Arknex.exe, Arknex.SDK.dll, bundled plugin binaries, native runtime dependencies, public text notes, SHA256SUMS.txt, and RELEASE-MANIFEST.json.

It must not contain source code, tests, development scripts, internal phase documents, local settings, logs, cache, database files, corpus files, or internal third-party audit manifests.

## Third-party and license compliance

Arknex uses a license-aware reuse model:

- Vendor: compatible components that can be integrated or redistributed with required notices.
- Wrap: components kept behind a helper or runtime boundary.
- Bridge: external workflows kept outside the core application.
- ReferenceOnly: projects used only as design, workflow, UX, or compatibility references.
- Pending: candidates that are not integrated until license status is clarified.

Key compliance notes:

- CUE4Parse is used as an Unreal parser foundation under Apache-2.0. Required notices are preserved in the runtime support directory when present.
- UAssetAPI is tracked as a MIT-licensed Unreal inspection foundation.
- AssetsTools.NET and several Unity ecosystem tools are tracked through the project license matrix and reuse policy.
- UnrealMappingsDumper is Bridge-class; injection-style behavior is not embedded into Arknex core.
- AddressablesTools remains pending until license status is clarified.

## FModel compliance

FModel is an important Unreal ecosystem reference, but it is GPL-3.0. Arknex treats FModel strictly as ReferenceOnly.

For this release:

- no FModel source code is copied into Arknex;
- no FModel binaries are redistributed;
- no FModel namespaces are expected in Arknex assemblies;
- no FModel assets or project files are shipped;
- no copied FModel implementation is included.

Arknex uses its own Avalonia UI, Host and SDK architecture, diagnostics, release packaging, and workspace descriptor model. Unreal handling is based on license-compatible components such as CUE4Parse and UAssetAPI, not FModel code.

## Known limitations

- This is a ZIP-based release; no installer or automatic updater is included.
- Code signing is not assumed, so Windows SmartScreen may warn on first launch.
- Developer SDK templates and sample source are not bundled as source in the end-user runtime package.
- Runtime capability enforcement is still a future hardening area; capabilities and trust are visible in diagnostics.
- Arknex Data Intelligence is included as a flagship prototype and SDK compatibility probe. Real-world text and localization linkage is not guaranteed for every title.

## Responsible use

Use Arknex only with content and projects you own, are authorized to inspect, or are legally permitted to process. Respect the licenses and terms that apply to your assets, tools, games, and dependencies.

---

## Arknex 日本語

Arknex は、Unity と Unreal のアセットを高速に閲覧、索引化、検索、プレビューし、SDK ベースの plugin で自由に拡張できる asset workbench です。

この repository は Arknex 1.0.0.0 (win-x64) の公開配布用 handoff です。開発用 source tree は含めず、公開用 README、checksum 情報、source-free な Windows runtime package または GitHub Releases asset への導線だけを置く想定です。

## Arknex とは

Arknex は、Unity / Unreal project の既存 asset を見つけやすく、確認しやすく、再利用しやすくするための desktop workbench です。単なる viewer ではなく、大きな project folder を scan して asset を index し、検索、詳細確認、preview、plugin workflow へつなげることを目的にしています。

Arknex の中心になる考え方は次の 3 つです。

1. Unity / Unreal 両対応の実用 asset viewer。
2. 大規模 project folder 向けの searchable index / asset workspace。
3. Arknex.SDK によって個人開発者が独自機能を追加できる plugin-first platform。

## 主な機能

- Unity と Unreal を 1 つの desktop workbench で扱う。
- project 登録、source scan、asset indexing。
- asset 一覧、検索、filter、詳細表示。
- 対応 asset の preview routing と、未対応 file の診断表示。
- 将来の export / automation に向けた workflow foundation。
- trust level、capability、contribution point、command、action、load failure を確認できる Plugin Diagnostics。
- first-party flagship prototype としての Arknex Data Intelligence。
- checksum と manifest による source-free release package 検証。

## SDK による拡張性

Arknex は Arknex.SDK と microkernel-style Host boundary を中心に設計しています。目標は、個人開発者が custom viewer、dashboard、report、validator、exporter、data workspace、project-specific helper を plugin として自由に作れる状態にすることです。

現在の公開 seam には、typed active project context、plugin workspace descriptor、structured action result、command / action diagnostics、read-only Host-indexed source access、capability / trust metadata、descriptor-driven workspace UI section があります。

基本方針は、共通 platform は Arknex core に置き、project 固有 workflow は plugin に分離することです。

## ダウンロードと checksum

Runtime package: Arknex-1.0.0.0-win-x64.zip

Checksum sidecar: Arknex-1.0.0.0-win-x64.zip.sha256

Expected SHA256: 731af77974b64b843f1a7a36e9003db308cfc8da1ac6de86ae7306d88abd53ec

初回起動前に PowerShell で checksum を確認してください。

    Get-FileHash -Algorithm SHA256 .\Arknex-1.0.0.0-win-x64.zip
    Get-Content .\Arknex-1.0.0.0-win-x64.zip.sha256

hash が一致しない場合は、ZIP を削除して再ダウンロードしてください。

重要: 生成される ZIP は GitHub の通常 repository file limit である 100 MiB を超える場合があります。その場合、ZIP は Git LFS で管理するか、repository には README と checksum を置き、ZIP は GitHub Releases の asset として添付してください。

## 使い方

1. Windows x64 runtime ZIP を download する。
2. SHA256 checksum を確認する。
3. ZIP を writable folder に展開する。
4. Arknex.exe と _arknex folder が同じ folder にあることを確認する。
5. Arknex.exe を起動する。
6. plugin が読み込めない場合は Plugin Diagnostics を確認する。

local smoke 済みの dist folder をそのまま配布しないでください。local run では settings、logs、cache、database などが生成されるため、public release package からは意図的に除外しています。

## 配布物の境界

runtime ZIP は allowlist staging から生成し、公開前に検証します。Arknex.exe、Arknex.SDK.dll、bundled plugin binaries、native runtime dependencies、public text notes、SHA256SUMS.txt、RELEASE-MANIFEST.json などの runtime files を含みます。

source code、tests、development scripts、internal phase documents、local settings、logs、cache、database、corpus、internal third-party audit manifest は含めません。

## 統合元ツールと license compliance

Arknex は Vendor / Wrap / Bridge / ReferenceOnly / Pending の reuse model で third-party component を管理します。

- Vendor: notice を保持して統合または再配布できる compatible component。
- Wrap: helper や runtime boundary の裏側で扱う component。
- Bridge: core に混ぜず、外部 workflow として扱うもの。
- ReferenceOnly: design、workflow、UX、compatibility の参考のみ。source code はコピーしない。
- Pending: license status が明確になるまで統合しない候補。

主な compliance 方針は次の通りです。

- CUE4Parse は Apache-2.0 の Unreal parser foundation として扱い、必要な notice を runtime support directory に保持します。
- UAssetAPI は MIT license の Unreal inspection foundation として扱います。
- AssetsTools.NET など Unity ecosystem tool は project license matrix と reuse policy に従って管理します。
- UnrealMappingsDumper は Bridge-class とし、inject 系の挙動を Arknex core に埋め込みません。
- AddressablesTools は license status が明確になるまで Pending とします。

## FModel compliance

FModel は Unreal ecosystem における重要な reference ですが、GPL-3.0 です。そのため Arknex では FModel を strict ReferenceOnly として扱います。

この release では次を守ります。

- FModel source code を Arknex にコピーしない。
- FModel binary を再配布しない。
- Arknex assembly に FModel namespace を含めない。
- FModel asset / project file を配布しない。
- FModel 実装のコピーを含めない。

Arknex は独自の Avalonia UI、Host / SDK architecture、diagnostics、release packaging、workspace descriptor model を持ちます。Unreal 対応は CUE4Parse や UAssetAPI など license-compatible component を基盤にしており、FModel code には依存しません。

## 既知の制限

- ZIP-based release であり、installer や automatic updater は含みません。
- code signing は未前提のため、Windows SmartScreen が初回起動時に警告する場合があります。
- end-user runtime package には developer SDK template や sample source は source として同梱しません。
- runtime capability enforcement は今後の hardening 項目です。capability と trust は diagnostics で確認できます。
- Arknex Data Intelligence は flagship prototype / SDK compatibility probe として同梱しています。全 title で text / localization linkage が完全に成立することは保証しません。

## 利用上の注意

Arknex は、自分が所有している、調査を許可されている、または法的に処理が許可されている content / project に対してのみ使用してください。asset、tool、game、dependency に適用される license と terms を尊重してください。
