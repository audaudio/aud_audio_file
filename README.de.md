# aud_audio_file

[English](README.md) | Deutsch

[![CI](https://github.com/audaudio/aud_audio_file/actions/workflows/quick_check.yaml/badge.svg)](https://github.com/audaudio/aud_audio_file/actions/workflows/quick_check.yaml)

Audiodateien für die Audanika Audio Engine: Decoder, Disk-Streaming-Player, Recorder, Offline-Bounce.

Teil der Audanika Audio Engine; geplant in
[aud_audio_pm](https://github.com/audaudio/aud_audio_pm). Das Paket ist
bisher ein Gerüst: Es baut seinen nativen Code auf iOS, Android, macOS,
Windows und Linux, aber keine der Funktionen seiner Beschreibung ist schon
umgesetzt.

## Motivation

Die Audanika Audio Engine rendert Graphen aus Nodes; Audiodateien zu lesen
und zu schreiben ist ein Anliegen für sich. Dieses Paket ist der Ort dafür
in der Familie: die Decoder, ein Player, der von der Platte streamt, ein
Recorder und ein Offline-Bounce, gebaut auf `aud_audio_graph`. Das Repo
wurde mit den anderen Repos der Engine angelegt und enthält das Gerüst
eines nativen Dart-Pakets; die Funktionen folgen in späteren Tickets.

## Installation

Das Paket ist nicht auf pub.dev veröffentlicht. Füge es als
Git-Abhängigkeit hinzu, aufgelöst über seinen Versions-Tag:

```yaml
dependencies:
  aud_audio_file:
    git:
      url: git@github.com:audaudio/aud_audio_file.git
      tag_pattern: "{{version}}"
    version: ^0.0.3
```

Dann `dart pub get` ausführen. Die native Bibliothek baut der Build-Hook
des Pakets, wenn die App gebaut wird.

## Verwendung

Die Bibliothek exportiert die zwei Funktionen der Vorlage für native
Pakete, eine kurzlebige und eine langlaufende, die auf einem Hilfs-Isolate
läuft. Das Beispiel in `example/` zeigt sie in einer Flutter-App:

```dart
import 'package:aud_audio_file/aud_audio_file.dart';

Future<void> main() async {
  // A short-lived native function, called on the main isolate
  print('sum(24, 18) = ${sum(24, 18)}');

  // A long-running native function, called on a helper isolate
  print('await sumAsync(24, 18) = ${await sumAsync(24, 18)}');
}
```

Es gibt aus:

```text
sum(24, 18) = 42
await sumAsync(24, 18) = 42
```

## Grenzen

- Decoder, Player, Recorder und Bounce sind noch nicht umgesetzt; die
  Bibliothek enthält nur die Vorlagenfunktionen `sum` und `sumAsync`
- Der native Code braucht eine native Plattform; das Paket kompiliert
  nicht fürs Web

## Dokumentation

- [Blog](doc/de/blog) — ein Beitrag pro Änderung
- [aud_audio_pm](https://github.com/audaudio/aud_audio_pm) — die Pläne und
  Entscheidungen der Audanika Audio Engine

## Status

Version 0.0.3, ein Gerüst. Vor 1.0 — die API kann sich zwischen
Minor-Versionen ändern.

## Mitwirken

- Folge dem [Develop-Guide](doc/guides/develop-guide.md), dem
  [Code-Guide](doc/guides/code-guide.md) und dem
  [Test-Guide](doc/guides/test-guide.md)
- Die Bindings neu erzeugen mit `dart run ffigen --config ffigen.yaml`
- Das Beispiel löst sich zusammen mit dem Paket in einem Pub-Workspace
  auf, damit ein Upgrade des Pakets auch das Beispiel aktualisiert

## Lizenz

MIT — siehe [LICENSE](LICENSE).
