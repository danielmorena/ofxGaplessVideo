# ofxGaplessVideo
Gapless Video Playback for OpenFrameworks. Runs with avFoundation on OSX and gStreamer on Linux. Use it with openFrameworks master, since the playback systems are loading clips faster than in the official release.

Usage
-----

ofxGaplessVideo is used for remote controlled video playback over the network. ofxGaplessVideo provides functions to preload movies flicker free and to trigger a new clip instantly, since it uses internally two video players and preloads the clips.

ofxGaplessVideo is thread safe, which means, the playback control can be run in an own thread. Normally, this will be a network listener thread which is listening for trigger and load signals.

Basic Functions in the Main Loop
--------------------------------

    /* Setup Function */
    MO.start();
    
    /* Update Function */
    MO.update();
    
    /* Draw Function (Fullscreen without Options */
    MO.draw()

Controlling Playback
--------------------

It's probably the most efficient way to pass the MO Object as a reference to a loader thread which is waiting for signals from a controller server.

Loads a Movie and starts playback immediately:

    MO->loadMovie(string movieFile, bool fade_in, bool fade_out);

Preloads a Movie:

    MO->appendMovie(string movieFile, bool fade_in, bool fade_out);

Starts a preloaded Movie. The parameter movieFile should be set to the same value as in appendMovie:

    MO->triggerMovie(string movieFile);

Communication
-------------

Either send loadMovie signals over the net if you want to start a clip by a single command. To create a more accurate system, send a preload signal first and a trigger signal in the moment you really want to start the movie.
