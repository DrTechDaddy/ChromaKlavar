ChromaKlavar Design Doc
ChromaKlavar is designed as a single client webpage.
The webpage consists of an HTML drawing surface, 
on whidh a staff and notes will be drawn.

Main sections of the code:
a <script> section consisting of javascript drawing routines
an html section:

HTML SECTION
* the first part is a number of arrays of parameters to customize the staff and notes
* the second part is a list js function called to draw individual notes 

In this program, the staff is assumed be vertical, like Klavarskribo

This design assumes a single grand staff for all parts;
individual parts (hands) may be distingushed by stem direction.
The staff is described by a list of midi numbers to be represented by lines
Staff lines can be distinguished by: line style, line width, and line color

A "song" is encoded in the function songMIDI as a series of midiCSV(...) calls.
Each call corresponds to a midi command.
The parameters of the midiCVS function are the values produced by the midiCSV utility
that converts the midi file to a human-readable .csv (commas separated value) text file.

midiCSV calls midiNote(...) to position and draw each note.
midiNote includes section to position and draw staff segments on the page;
for the very first note, and if a note would go past the bottom of the allotted space on the page,
it calls functions to draw a staff segment in the next available area of the page.
At present, the limit is one page, but more "pages" could be added.

In this program, it is assumed that time is linear;
Note heads are positioned at "incident time".
Duration is implicit; a note ends when the next note in the part begins.
Bar lines are ignored for note duration.
For rests, a "stop" symbol included.
To indicate that a note continues to sound when another note is added, a "continue" symbol is included.

This program assumes "shape notes", that is, a different note-head symbol for each of the 12TET tone in the "octave".
In addition to distinct symbols, each chromatic tone may have a distinct color and fill (open, solid, shaded).

These staff, notehead, and stem options allow customization for a variety of Anternative Notations on the MNP website.
It specifically accommodates approximations to Klavarskribo, ExpressStave, and Clairnote, as well as Chromatonnetz.
NOTE: the program does not include provision for representing note duration with the note symbol, e.g. flags, beams, dots, etc., so it cannot be used for Traditional Notation.

Note position is based on MIDI values
* pitch is denoted by MIDI number
* time is denoted by measure number and "tick"
    ticks per quarter note (TPQN) is a MIDI value relating ticks 
    to note duration.
* the Time Signature MIDI command is used to convey information relating ticks to musical note duration.

SCRIPT SECTION:
The script uses HTML canvas tags to draw staff lines and notes.
Position and characteristics of staff lines are determined from arrays in the HTML data

NOTE: the function satb(...) is a "built-in" song for developmental testing; it is commented out for scoring actual songs.