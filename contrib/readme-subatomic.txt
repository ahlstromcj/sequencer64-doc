http://www.subatomicglue.com/seq24/readme-subatomic.txt

==============================================================
beta1
==============================================================

Win32:
This is rob's win32 code from 0.8.7 (which was never checked in)
It is merged with revision 48 from bazaar (something like release version 0.9.0)

Thoughts:
 - hey, it's portmidi, isn't this cross platform, should seq24
   use this all the time instead of the linux-only Alsa/Jack combo??
   or at least win32/osx (hey this means seq24 may port to OSX now!)

==============================================================
beta2
==============================================================

==============================================================
SPACEBAR start/stop the sequencer

There's a new key binding for SPACEBAR to start/stop the
sequencer in all the views.


==============================================================
New Midi Clock input:

seq24 will slave off of incoming MidiClock messages
0xfc 0xfa 0xf8   (start stop and tick)

This has been tested with another seq24 instance (stop/start works)
This has been tested with a x0xb0x in (start/stop works)

It will also pay attention to 0xfb (continue) and 0xf2 (Midi Song Pos) but
these aren't tested...

Currently there's no way to adjust a time offset... :(

==============================================================
New Mouse Controls:
"Fruity Mode"  (like the fruityloops piano roll mouse interaction)
(selectable in options menu, in .seq24rc, and on command line)

Sequencer Roll:

Pencil (draw) or Selection (context sensitive)
 - Left click on empty space
   adds a note

 - Left click on note
   toggles note selection
 - Left click move from empty space
   draw many notes while moving ptr
 - Left click move on a note
   moves/grows the selected note depending on where pointer is

Think of Ctrl like a selection modifier to default pencil ptr
 - Left Ctrl click on empty space
   deselect all selected notes

 - Left Ctrl click on note
   adds to selection
 - Left Ctrl click move in empty space
   starts selection box that only selects what's inside on button up
 - Left Ctrl click move on a note
   make a copy of the selection (does copy/paste of selected notes)

Think of Shift like an "add to selection" modifier
 - Left Ctrl Shift click on empty space
   nothing

 - Left Ctrl Shift click on note
   adds to selection
 - Left Ctrl Shift click move in empty space
   starts selection box that toggles selection on button up
 - Left Ctrl Shift click move on a note
   make a copy of the selection (does copy/paste of selected notes)

Think of Right Click like an eraser or easy selection...
Eraser
 - Right click on note
   deletes note...  if you drag the mouse around it will delete other notes too.
 - Right+Ctrl click on note
   delete all selected notes at once time including under the cursor

Selection:
 - Right click on empty space
   deselect all notes
 - Right+Ctrl click on empty space
   nothing
 - Right click move from empty space
   starts selection box that sets selection only to the notes inside it
 - Right+Ctrl click move from empty space
   starts selection box that toggles selection on notes inside it


Song Editor Window:
 - is kinda similar to the SequencerRoll mouse buttons, though more limited
   due to how the editor works...   you'll figure it out. :)


Also added:
 - Ctrl A :  select All
 - Space bar starts/stops the main window's playback...

======================================================================
beta3

altefrequenzy's mute groups patch



======================================================================
beta4

crash fix when pasting in main window without previously doing a copy
 - the clipboard didn't have a midi channel set, playing any notes to this
   resulted in a crash

file/options/(keyboard tab)  menu
 - GUI for editing keybindings

L button in main window
 - lets you save mute groups into one of the mutegroup keys (see keyboard tab)
 - highlights when "learn" is active.
 - see also the Insert key (default key for mute group learn),
   hold it down while pressing a mute group key to assign
 - Learn Key also toggles the main window's L button visually...

confirmation(or error) dialogs for assigning mute group keys
 - it was very confusing before when it failed silently, now it is clear.

.seq24rc file:
 - now has better comments for keybindings
   i.e.
       97 2   # 'a'
- fix for the Number of [keyboard-control] keys:
   not hardcoded to 32 but actual number of keys that follow, same
   for [keyboard-groups].  it should always be 32, but i think i had a partial
   write happen once that screwed up something resulting in nothing in the
   map, but there was a 32 there, so it happily read values from later in the
   file...   rare bug, probably happened because i killed the app in the middle
   of writing...


on the main window, each sequencer box now has a label that shows
  the keybinding to toggle mute/unmute
 - enabled by default
 - can disable in the new Keyboard options

tooltips for UI elements now work, when using older versions of GTK.

fix sequencer start/stop keybinding to work with SPACEBAR for both
start AND stop, consistently across all UIs (main window, sequencer
editor, song editor).
 - some UIs before were hard coded to SPACEBAR, (i think i did this in seqroll)
 - some UIs did not support SPACEBAR bound to both start and stop (as a toggle)
 - key_start and key_stop now in .seq24rc (also in Keyboard options tab)

command line "show keys" option now also shows the name of the key you typed
rather than only the keycode
i.e.     97 == 'a'

sync'd the .seq24usr loader with the .sec24rc loader (mute groups, etc..)
 - also updated it for the other keybindings, not present before
   bpm up/dn, keyscreenset, start/stop...
 - it turns out this is all ifdef 0'd out anyway, so... sorry,
   it's not really available .. but at least the 2 code files are sync'd! :)

