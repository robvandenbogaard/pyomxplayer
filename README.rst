pyomxplayer
===========
Python wrapper module around `OMXPlayer <https://github.com/huceke/omxplayer>`_
for the Raspberry Pi.

Unlike `other implementations <https://github.com/KenT2/pyomxplayer>`_, this
module does not rely on any external scripts and FIFOs, but uses the
`pexpect module <http://pypi.python.org/pypi/pexpect/2.4>`_ for communication
with the OMXPlayer process.

CPU overhead is rather low (~3% for the Python process on my development RPi)
and the object-oriented design makes it easy to re-use in other projects.

Installation:
(assuming you're the pi user and you want to install system wide!)
-------------
::

    git clone https://github.com/karlg100/pyomxplayer.git
    pushd pyomxplayer
    sudo python setup.py install
    popd

Example:
--------
::

    >>> from pyomxplayer import OMXPlayer
    >>> from pprint import pprint
    >>> omx = OMXPlayer('/tmp/video.mp4', '--no-osd')
    >>> pprint(omx.__dict__)
	{'_info_process': <pexpect.spawn object at 0x76a14390>,
	 '_position_thread': <Thread(Thread-1, started 1989665904)>,
	 '_process': <pexpect.spawn object at 0x76a14350>,
	 '_spawn': <class 'pexpect.spawn'>,
	 '_stop_callback': None,
	 'audio': {'bps': 16, 'channels': 2, 'decoder': 'aac', 'rate': 48000},
	 'current_volume': 0,
	 'duration': 5894210000L,
	 'info_output_buffer': None,
	 'media_file': 'Wall-E.m4v',
	 'muted': False,
	 'parser': <pyomxplayer.parser.OMXPlayerParser object at 0x76a14430>,
	 'paused': True,
	 'position': 0.0,
	 'subtitles_visible': False,
	 'title': 'Wall-E',
	 'video': {'decoder': 'omx-h264',
		   'dimensions': (720, 360),
		   'fps': 25.0,
		   'profile': 100}}
    >>> omx.toggle_pause()
    >>> omx.position
    9.43
    >>> omx.toggle_mute(.1)
    >>> omx.stop()
