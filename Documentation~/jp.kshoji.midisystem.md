# How to use this library
At first, setup the library to Unity Project. 
Open the `manifest.json` for your project and add the following entry to your list of dependencies.

```json
"jp.kshoji.midisystem": "https://github.com/kshoji/MidiSystem-for-.NET.git",
```

## Read a Standard MIDI File, and get Sequence
```cs
// Read file content with stream
using var stream = new FileStream(smfPath, FileMode.Open, FileAccess.Read);

// Read MIDI sequence from stream
var sequence = MidiSystem.ReadSequence(stream);
```

## Play the Sequence with Sequencer
```cs
// Sequencer initialization
var isSequencerOpened = false;
var sequencer = new SequencerImpl(() => { isSequencerOpened = true; });
sequencer.Open();

...

// Wait until the sequencer will be opened.
if (isSequencerOpened)
{
    // Update connected MIDI device informations
    sequencer.UpdateDeviceConnections();

    // Set the MIDI sequence
    sequencer.SetSequence(sequence);

    // Start to play MIDI sequence
    sequencer.Start();

    ...

    // Stop playing
    sequencer.Stop();
}
```

## Record MIDI data to Sequence with Sequencer
```cs
// Sequencer initialization
var isSequencerOpened = false;
var sequencer = new SequencerImpl(() => { isSequencerOpened = true; });
sequencer.Open();

...

// Wait until the sequencer will be opened.
if (isSequencerOpened)
{
    // Update connected MIDI device informations
    sequencer.UpdateDeviceConnections();

    // Create new sequence, and track
    var sequence = new Sequence(Sequence.Ppq, 480);
    var track = sequence.CreateTrack();

    // Setup track to enable recording MIDI data
    sequencer.SetRecordEnable(track, -1);

    // Set the created sequence to sequencer
    sequencer.SetSequence(sequence);

    // Start to record MIDI sequence
    sequencer.StartRecording();

    ...

    // Stop recording
    sequencer.StopRecording();
}
```

## Write Sequence to a Standard MIDI File
```cs
// Get recorded sequence
var sequence = sequencer.GetSequence();
if (sequence.GetTickLength() > 0)
{
    // Write the sequence to the MIDI file
    using var stream = new FileStream(smfPath, FileMode.OpenOrCreate, FileAccess.Write);
    MidiSystem.WriteSequence(sequence, stream);
}
```
