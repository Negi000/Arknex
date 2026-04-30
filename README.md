# Arknex

[English](#arknex-english) | [日本語](#arknex-日本語)

---

## Arknex (English)

**Arknex** is a Windows desktop **asset workbench** for browsing, indexing, searching, and previewing assets from Unity and Unreal projects, with an SDK-first plugin platform that lets developers extend it with custom workflows.

This repository is the **public-facing handoff page** for Arknex. The development source tree, internal documents, audit manifests, and unreleased components are kept private. Releases of the runtime are published as attachments on the GitHub **Releases** page rather than committed to this repository.

### Latest release

- Version: `1.0.0.0` (Windows `win-x64` self-contained build)
- Runtime ZIP: `Arknex-1.0.0.0-win-x64.zip`
- SHA-256: `9c2ccb1da0fd69c26c39844430afcc166590ce694ba8ec794ce4cc787abcd621`
- Download and verify from the official Releases page:
  https://github.com/Negi000/Arknex/releases/tag/v1.0.0.0

The ZIP is not committed to this repository. Always download it from the Releases page above so the published SHA-256 and the file you run can be cross-checked.

### What Arknex is

Arknex is a desktop application for individual developers and small teams who need a faster, more organized way to inspect and reuse the assets they already have permission to work with. Instead of bolting project-specific behavior onto a single tool, Arknex separates a stable application core from project-specific behavior implemented as plugins on top of **Arknex.SDK**.

The product focuses on three pillars:

1. A **practical viewer** for Unity and Unreal asset folders.
2. A **searchable index and asset workspace** for large project trees.
3. An **SDK-first plugin platform** so each developer can build the workflow they actually need.

### Highlights

- Unified Windows workbench for Unity and Unreal asset folders.
- Project registration, source scanning, and asset indexing.
- Asset list, search, filtering, and detailed metadata view.
- Preview routing for supported asset categories (textures, audio, text, scripts, animation data, etc.) with graceful diagnostics for unsupported files.
- Foundations for export and batch workflows (more arrives in future releases).
- **Plugin Diagnostics** view with trust level, capabilities, contribution points, command/action diagnostics, and load-failure reporting.
- Self-contained Windows x64 ZIP — no .NET install required.
- Source-free release packaging validated by allowlist before publication, with embedded `SHA256SUMS.txt` and `RELEASE-MANIFEST.json` for per-file integrity.
- Localization framework for Japanese, English, Chinese (Simplified), Korean, and Russian UI strings.

### SDK and plugin platform

Arknex is built around **Arknex.SDK** and a microkernel-style Host boundary. The goal is open extensibility: a developer can add their own viewers, dashboards, validators, exporters, data workspaces, or project-specific helpers as plugins, without modifying the core application.

Public extension surfaces include:

- typed active project / version context;
- descriptor-driven plugin workspace UI (fields, tables, graphs, progress, actions);
- structured action results and command/action diagnostics;
- read-only Host-indexed source access from plugins;
- declared capability and trust metadata per plugin.

A small reference plugin (`Arknex.Samples.MinimalPlugin`) ships with the runtime to demonstrate manifest, contributions, UI command, and descriptor-driven workspace patterns. Full SDK source, project templates, and additional sample plugins are not part of the end-user runtime ZIP.

### Quick start

1. Open the Releases page above and download both the `.zip` and its `.zip.sha256` sidecar.
2. Verify the checksum in PowerShell:

   `powershell
   Get-FileHash -Algorithm SHA256 .\Arknex-1.0.0.0-win-x64.zip
   Get-Content .\Arknex-1.0.0.0-win-x64.zip.sha256
   `

   The two hashes must be identical (case-insensitive). If they do not match, delete the ZIP and download it again.
3. Extract the ZIP into a writable folder (avoid `C:\Program Files`).
4. Keep `Arknex.exe` and the `_arknex` folder side by side.
5. Run `Arknex.exe`.
6. If a plugin fails to load, open **Plugin Diagnostics** to inspect trust, capabilities, and load failures.

Arknex stores its local settings, logs, cache, and database under `_arknex/` next to the executable. Back up that folder before upgrading if you want to keep your project registrations.

### System requirements

- Windows 10 or later, x64.
- A modern x64 CPU; no specific minimum is enforced.
- Around 1–2 GB of free RAM during indexing of large projects, plus disk space for the cache and any exports you create.
- A GPU capable of basic OpenGL/Direct3D (used for texture preview).

The required .NET 8 runtime is bundled inside the self-contained ZIP. No separate installer is needed.

### Distribution boundary

The runtime ZIP is generated from an allowlisted staging layout and validated before publication.

- **Included**: `Arknex.exe`, `Arknex.SDK.dll` and its XML documentation, the bundled sample plugin, native runtime dependencies, third-party notices required by their licenses, and integrity files (`SHA256SUMS.txt`, `RELEASE-MANIFEST.json`).
- **Excluded**: source code, tests, build scripts, internal phase / design / audit documents, local user settings, logs, caches, databases, project corpora, and any plugins flagged as unreleased or commercial-only (such as the in-development `Arknex.Plugins.DataIntelligence`).

### Disclaimer

Arknex is provided **as is**, without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and non-infringement. The authors are not liable for any claim, damage, or other liability arising from the use of this software.

By downloading or running Arknex, you accept the following:

1. **You are solely responsible** for ensuring that you have the legal right — by ownership, license, contract, or applicable law — to inspect, decode, view, copy, modify, export, or otherwise process every file you open with Arknex.
2. Arknex is a **general-purpose desktop tool**. It does **not** include game-specific decryption keys, per-title cryptographic parameters, hardcoded encryption schemes, or mapping dumps for any commercial title. It will not bypass any technical protection measure on your behalf.
3. Arknex must not be used to violate end-user license agreements, terms of service, intellectual-property rights, anti-cheat policies, regional laws, or any other obligations that apply to the assets, games, engines, or platforms you work with. The authors do not endorse and do not provide support for use of this tool against content you are not authorized to handle.
4. The maintainers reserve the right to refuse support, accept contributions, or distribute changes that, in their judgement, would primarily enable misuse.

### Third-party software

Arknex bundles or links to a number of open-source components. Their respective licenses and notices are authoritative; the summary below is informational.

- `Avalonia` and the `Avalonia.*` UI stack — MIT.
- `CommunityToolkit.Mvvm` — MIT.
- `Dapper`, `Microsoft.Data.Sqlite`, `Microsoft.Extensions.DependencyInjection` — MIT (Microsoft / .NET Foundation).
- `Serilog` and Serilog sinks — Apache-2.0.
- `SkiaSharp` — MIT.
- `SharpGLTF.Core` — MIT.
- `NAudio`, `NVorbis`, `NAudio.Vorbis` — MIT / Ms-PL family.
- `LibVLCSharp` and `VideoLAN.LibVLC.Windows` — LGPL-2.1+ (LibVLC) and the LibVLCSharp wrapper license; the native LibVLC binaries remain governed by the VideoLAN project.
- `CUE4Parse` and `CUE4Parse-Conversion` — Apache-2.0. The required `NOTICE` file is preserved in the runtime support directory of the release ZIP.
- `UAssetAPI` — MIT.
- `AssetsTools.NET` and additional MIT-family Unity-side helpers (e.g. `AnimeStudio`, `RazTools-*`, `AssetStudioPangu`) — MIT.

Arknex deliberately treats certain ecosystem projects as **reference-only**:

- **FModel** is GPL-3.0 and is **not** bundled, vendored, linked, or reimplemented from source. It is acknowledged only as a high-level UX/workflow reference. No FModel code, binaries, namespaces, or assets are shipped with Arknex.
- **UnrealMappingsDumper** is treated as a Bridge-class external workflow; injection-style behavior is not embedded into Arknex core.
- **AddressablesTools** is currently held as Pending until its license status is fully clarified in the project audit.

A more detailed compliance summary is published in the runtime ZIP and on the GitHub Releases page.

### Trademarks

Unity is a trademark or registered trademark of **Unity Technologies**. Unreal and Unreal Engine are trademarks or registered trademarks of **Epic Games, Inc.** All other trademarks belong to their respective owners. Arknex is an independent project and is **not** developed, endorsed, sponsored, or affiliated with Unity Technologies, Epic Games, or any game publisher.

---

## Arknex 日本語

**Arknex** は Unity / Unreal の asset を閲覧・索引化・検索・preview するための Windows desktop **asset workbench** です。SDK-first な plugin platform を中心に設計されており、開発者は独自の workflow を plugin として追加できます。

この repository は、Arknex の **公開向け案内ページ** です。開発用の source tree、内部設計文書、audit manifest、未リリースの component などはこの repository には含めません。runtime の配布物は、この repository に直接 commit せず、GitHub の **Releases** ページに asset として添付して公開します。

### 最新リリース

- バージョン: `1.0.0.0` (Windows `win-x64` self-contained build)
- Runtime ZIP: `Arknex-1.0.0.0-win-x64.zip`
- SHA-256: `9c2ccb1da0fd69c26c39844430afcc166590ce694ba8ec794ce4cc787abcd621`
- 公式 Releases ページから download / 検証してください:
  https://github.com/Negi000/Arknex/releases/tag/v1.0.0.0

ZIP 本体は repository に commit していません。Releases ページに記載された SHA-256 と、手元で計算した hash を必ず照合してから利用してください。

### Arknex とは

Arknex は、自分の権利範囲で扱える Unity / Unreal asset を、より速く、より整理された形で扱いたい個人開発者・小規模チーム向けの desktop application です。project 固有の処理を 1 つのツールに直接書き足していくのではなく、安定した application core と、**Arknex.SDK** で動く project 固有 plugin とを明確に分離しています。

product は次の 3 本柱を中心に設計されています。

1. Unity / Unreal asset folder のための **実用的な viewer**。
2. 大規模 project tree のための **検索可能な index / asset workspace**。
3. 各開発者が必要な workflow を実装するための **SDK-first plugin platform**。

### 主な特徴

- Unity と Unreal を 1 つの workbench に統合。
- project 登録、source scan、asset indexing。
- asset 一覧、検索、filter、詳細表示。
- 対応 asset カテゴリ (texture / audio / text / script / animation data など) の preview routing と、未対応 file の診断表示。
- 将来の export / batch workflow のための foundation。
- trust level、capability、contribution point、command / action diagnostics、load failure を確認できる **Plugin Diagnostics**。
- self-contained な Windows x64 ZIP (.NET の別途 install 不要)。
- 公開前 allowlist 検証付きの source-free release packaging。`SHA256SUMS.txt` と `RELEASE-MANIFEST.json` を ZIP 内に同梱して per-file integrity を確認可能。
- 日本語 / 英語 / 中国語 (簡体) / 韓国語 / Russian の UI string framework。

### SDK と plugin platform

Arknex は **Arknex.SDK** と microkernel 的な Host boundary を中心に構築されています。目的は、core を改造せずに、各開発者が独自の viewer / dashboard / validator / exporter / data workspace / project 固有 helper を plugin として自由に追加できる状態を保つことです。

公開されている主な extension surface:

- typed な active project / version context;
- descriptor-driven な plugin workspace UI (field / table / graph / progress / action);
- structured な action result と command / action diagnostics;
- plugin から利用できる Host-indexed read-only source access;
- 各 plugin が宣言する capability / trust metadata。

reference として `Arknex.Samples.MinimalPlugin` を runtime に同梱しており、manifest、contribution、UI command、descriptor workspace の最小実装を確認できます。SDK 本体の source、project template、追加 sample plugin は end-user runtime ZIP には含めません。

### Quick start

1. 上記 Releases ページから `.zip` と `.zip.sha256` の両方を download します。
2. PowerShell で SHA-256 を検証します:

   `powershell
   Get-FileHash -Algorithm SHA256 .\Arknex-1.0.0.0-win-x64.zip
   Get-Content .\Arknex-1.0.0.0-win-x64.zip.sha256
   `

   両方の hash が大文字小文字を無視して一致することを確認してください。一致しない場合は ZIP を削除して再 download します。
3. ZIP を書き込み可能な folder に展開します (`C:\Program Files` 配下は避けてください)。
4. `Arknex.exe` と `_arknex` folder を必ず同じ folder に置いてください。
5. `Arknex.exe` を起動します。
6. plugin の load に失敗した場合は **Plugin Diagnostics** を開き、trust / capability / load failure を確認してください。

Arknex の local settings、log、cache、database は `_arknex/` 配下に作られます。upgrade の前に、必要な project 登録などはこの folder を backup しておいてください。

### 動作環境

- Windows 10 以降、x64。
- 最近の x64 CPU (明示的な最低スペックはありません)。
- 大規模 project の indexing 中は 1〜2 GB 程度の空き memory、加えて cache や export 用の disk 容量。
- texture preview のために OpenGL / Direct3D が動作する GPU。

必要な .NET 8 runtime は self-contained ZIP に同梱されているため、別途 install する必要はありません。

### 配布物の境界

runtime ZIP は allowlist staging から生成し、公開前に検証しています。

- **含むもの**: `Arknex.exe`、`Arknex.SDK.dll` とその XML document、同梱 sample plugin、必要な native runtime、各 license が要求する third-party notice、integrity 用の `SHA256SUMS.txt` と `RELEASE-MANIFEST.json`。
- **含まないもの**: source code、test、build script、内部の phase / design / audit document、local user settings、log、cache、database、project corpus、未公開・商用扱いの plugin (例: 開発中の `Arknex.Plugins.DataIntelligence`) など。

### 免責事項

Arknex は **現状のまま (AS IS)** 提供されます。明示・黙示を問わず、商品性、特定目的への適合性、第三者の権利を侵害しないことを含む一切の保証を行いません。本 software の使用に関連して生じた直接・間接の損害について、作者および貢献者は一切の責任を負いません。

Arknex を download または使用する時点で、利用者は以下に同意したものとみなします。

1. Arknex で開く全ての file について、所有権・license 契約・契約上の許諾・適用法律のいずれかにより、自分が **合法的に閲覧・解析・複製・改変・export・処理する権利を持っていること** を保証する責任は、利用者自身にあります。
2. Arknex は **汎用 desktop tool** であり、特定の game / title 向けの decryption key、暗号 parameter、hardcode された暗号 scheme、mapping dump などは **一切同梱しません**。利用者の代わりに技術的保護手段 (TPM) を回避することはありません。
3. Arknex は、end-user license agreement、利用規約、知的財産権、anti-cheat policy、各国法令、その他 asset / game / engine / platform に適用される義務に違反する目的で使用してはなりません。作者は、利用者が権利を持たない content への利用を推奨せず、その用途に対する support も行いません。
4. 上記方針に反すると判断される利用、issue、contribution、配布変更については、作者の判断で support、受け入れ、配布の停止を行うことがあります。

### Third-party software

Arknex は多数の OSS component を bundle / link しています。各 license と notice 本文が常に正であり、以下は参考情報です。

- `Avalonia` および `Avalonia.*` UI stack — MIT。
- `CommunityToolkit.Mvvm` — MIT。
- `Dapper`、`Microsoft.Data.Sqlite`、`Microsoft.Extensions.DependencyInjection` — MIT (Microsoft / .NET Foundation)。
- `Serilog` および sink — Apache-2.0。
- `SkiaSharp` — MIT。
- `SharpGLTF.Core` — MIT。
- `NAudio`、`NVorbis`、`NAudio.Vorbis` — MIT / Ms-PL 系。
- `LibVLCSharp`、`VideoLAN.LibVLC.Windows` — LibVLC 本体は LGPL-2.1+、LibVLCSharp wrapper はその独自 license。native LibVLC binary の権利は VideoLAN project に帰属します。
- `CUE4Parse` および `CUE4Parse-Conversion` — Apache-2.0。release ZIP の runtime support directory に必要な `NOTICE` file を保持します。
- `UAssetAPI` — MIT。
- `AssetsTools.NET` および MIT 系の Unity-side helper (例: `AnimeStudio`、`RazTools-*`、`AssetStudioPangu` 等) — MIT。

以下の project については、Arknex として明示的に **reference-only** 扱いとしています。

- **FModel** は GPL-3.0 です。Arknex には bundle / vendor / link / source 流用のいずれも行わず、UX や workflow の高レベル参考としてのみ言及します。FModel の code、binary、namespace、asset を release ZIP に含めることはありません。
- **UnrealMappingsDumper** は Bridge-class の外部 workflow として扱い、inject 系の挙動を Arknex core に埋め込みません。
- **AddressablesTools** は license status が project audit で明確化されるまで Pending 扱いです。

詳細な compliance summary は runtime ZIP 内および GitHub Releases ページに掲載しています。

### 商標

Unity は **Unity Technologies** の商標または登録商標です。Unreal および Unreal Engine は **Epic Games, Inc.** の商標または登録商標です。その他の商標はそれぞれの権利者に帰属します。Arknex は独立した project であり、Unity Technologies、Epic Games、いずれの game publisher とも開発・後援・提携関係にありません。
