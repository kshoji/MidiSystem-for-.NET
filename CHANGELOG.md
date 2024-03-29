# Changelog
All notable changes to this package will be documented in this file.

## [1.0.2] - 2022-08-29

### Update release

* Fix issues
  * Sequencer thread remains after closing
  * Use Monitor.Wait/Pulse instead of Thread.Sleep/Interrupt
  * SMF read/write issues around System exclusive

## [1.0.1] - 2022-03-01

### Update release

* Fix compile errors on C# 7.3 (Unity 2019)

## [1.0.0] - 2022-02-26

### Update release

* Add .NET solution/project files
* Update documentation
* Fix issues
  * SMF reading/writing issues
  * pause/resume issue

## [0.0.0] - 2022-02-09

### This is the pre-release of MidiSystem.

* Initial release.
* Ported Sequencer, StandardMidiFileReader, StandardMidiFileWriter from `javax.sound.midi package`, to C#.
* No dependency with Unity, so it also runs on pure .NET environment.
