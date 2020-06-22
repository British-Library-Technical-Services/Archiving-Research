**Audio fingerprinting as a method to find duplicate content**

_22 June 2020_ Tom Ruane [tom.ruane@bl.uk](mailto:tom.ruane@bl.uk)

**Background**

As technology develops or becomes obsolete it is vital for an audiovisual archive to ensure ongoing access to its content through format migration.  The British Library has been digitally archiving audio since the mid-80s, first on PCM encoded Betamax, through to CD-R and now WAV file.

As part of our migration planning we need to assess if duplicated content exists in our digitised archive and decide, if multiple do copies exist, which represents the most complete and accurate version.  Due to the increasingly large volumes of data we manage, it would be very useful to develop an automated method in our workflows to achieve this.

Audio Fingerprinting measures the sonic attributes of an audio signal through Fast Fourier Transform (FFT) and / or peak analysis, the resulting “fingerprint” can then be compared against another set of signals to find a match; this can be done to simply compare two files against each other or across a large dataset.  The most well-known implementation of fingerprinting is the app [Shazam](https://www.shazam.com), which allows users to identify a piece of music simply by holding their phone to a speaker and recording a short section of the audio.

Commercial services like Shazam are designed with the specific purpose of identifying “songs”, quickly, and cannot be used against a local, user-generated dataset.  However, there are similar open source tools available that can be implemented in a local environment.

With this in mind I have done some initial research to assess the current landscape to see if audio fingerprinting is potentially useful for an audio archive and worth pursuing to further aid our workflows.

**Chromaprint**

The most well known, non-commercial use of audio fingerprinting is in MusicBrainz’s [AcoustID](https://acoustid.org/fingerprinter); developed by Lukáš Lalinský.

There are several stages to the identification process, including hashing the fingerprint to create a unique ID and querying the MusicBrainz online database, but the actual fingerprint generation is done locally using the stand-alone tool [Chromaprint](https://acoustid.org/chromaprint).

The developer has written a very easy to read primer on how the Chromaprint algorithm works in this blog post: [How does Chromaprint work?](https://oxygene.sk/2011/01/how-does-chromaprint-work/)

There is an active community around MusicBrainz and Python bindings have been written for the Chromprint API in the form of [pyacoustid,](https://pypi.org/project/pyacoustid/) which makes it fairly quick and easy to get up and running, with just a few lines of code.  The AcoustID system was created specifically to match data across the MusicBrainz database though, so there is no in-built functionality to compare a local set of fingerprints generated through Chromaprint.

The following [blog](https://yohanes.gultom.me/2018/03/24/simple-music-fingerprinting-using-chromaprint-in-python/) posted by [Yohanes Gultom](mailto:yohanes.gultom@gmail.com) implemented comparison using “fuzzy” (approximate) string matching via the Python module [Fuzzywuzzy](https://pypi.org/project/fuzzywuzzy/), which uses [Levenshtein distance](https://en.wikipedia.org/wiki/Levenshtein_distance) to calculate strings differences (code example below).  It is important to point out here that fingerprints are blocks of data, representing the measurement of frequency over time.  Though this data can be transcoded into a spectrogram for visualisation, it is not (typically) how comparison is done.  It it much more effective and efficient to compare matching patterns in the data through string analysis techniques.

    #python modules imports
	import acoustid
	import chromaprint
	import numpy as np
	import matplotlib.pyplot as plt
	from fuzzywuzzy import fuzz
	
	#generate fingerprint for source file
	duration, fp_encoded = acoustid.fingerprint_file("source.wav")
	fingerprint, version = chromaprint.decode_fingerprint(fp_encoded)
	
	#generate fingerprint for target file to compare
	duration, fp_encoded = acoustid.fingerprint_file("target.wav")
	sample_fingerprint, version = chromaprint.decode_fingerprint(fp_encoded)
	
	#use to view bitmap of fingerprint (not necessary for comparison)
	fig = plt.figure()
	bitmap = np.transpose(np.array([[b == '1' for b in list('{:32b}'.format(i & 0xffffffff))] for i in fingerprint]))
	plt.imshow(bitmap)
	plt.show()

	#calculate similarity ratio between fingerprints
	similarity = fuzz.ratio(sample_fingerprint, fingerprint)
	print(similarity)

The main drawbacks to Chromaprint (for our use case) are inherent in its design, similar to Shazam it is designed to quickly match “songs” and, as stated by the author, is less effective with other content types (though from my testing it was able to match speech recordings without problem).  To maintain quick operation, Chromaprint also limits its analysis of the audio signal to the first 2 minutes only, so anything beyond that point is not accounted for. It is also unable to compensate for any type of signal offset, so a file with 30 seconds of silence at the start will not be matched to the same exact recording with no offset.

 Again, all the points raised, are by design to accomplish its intended task effectively.  Being open source, the code is freely available so I’m sure someone with the correct technical knowledge would be able to edit these attributes to better meet their needs (I’m not that person!).

**xcorrSound**

This is a suite of tools developed by the State and Univeristy Library, Denmark to find overlapping sections of audio in their digitised archive; see more details here - [http://xcorrsound.openpreservation.org](http://xcorrsound.openpreservation.org)

There are three tools included: _sound-match_, _waveform-compare_ and _overlap-analysis_.  Full details on each tool can be found in the above link, but from my testing _overlap-analysis_ was the only tool I found to be effective in anything other than matching exact copies.

The xcorrSound suite utilises cross-correlation to measure signal similarities based on their relative offset; put (very) simply it runs one signal along the other to highlight if / where the signal peaks match.  So unlike the other tools discussed it does not generate a fingerprint but actually runs real-time analysis on the audio signals.

There are various blog posts written by the authors but not a huge amount of technical detail is included; the [GitHub repository](https://github.com/openpreserve/scape-xcorrsound) is sparse with very few code examples given.  The tools were designed and implemented for a specific task for the University Library and don’t really have scope beyond that. 

With the dependencies installed, overlap-analysis can be run with a single line of code:

  	overlap-analysis source.wav target.wav

However, though simple and limited to a single output - _overlap-analysis_ was quite effective at finding matching audio within much longer recordings.  A good use case for us would be locating a single edited piece of music from a longer concert or album, for example.  It was still effective at finding matches, even after audio manipulation had been applied to the recording to mimic real-world variations in the source material (such as reduced high-end or added noise); however, this would require further testing to get a clearer picture of its limits.

The major drawback to overlap-analysis is that it cannot match content recorded at different sample rates; as the analysis is dependent on lining up two signals, a reduced (or increased) number of sample points make this impossible.  Also, as it is running ‘live’ analysis on the actual audio files, it is quite slow and would likely take a long time run across a large amount of content.

**Dejavu**

A tool described by its author as an open-source alternative to Shazam.  It is well documented and seems to have an active user base, though development activity appears to have stopped around 2014 (though updates have appeared recently).  It is designed to run comparisons against large, local datasets and is able to compensate for noise and interference outside of the wanted signal.  It has Python bindings and I believe, once setup correctly, would be simple to use.  I unfortunately wasn’t able to get all the dependencies correctly installed, so I was unable to to test it on any examples.  Given more time I would probably be able to get it up and running, but after much head scratching I had to leave it.  Accounts of its effectiveness around the web are positive so I think further research would be worthwhile.  An excellent blog written by the author can be found here - [https://willdrevo.com/fingerprinting-and-audio-recognition-with-python/](https://willdrevo.com/fingerprinting-and-audio-recognition-with-python/)

GitHub repository - [https://github.com/worldveil/dejavu](https://github.com/worldveil/dejavu)

**Conclusion**

Even with the relatively short amount of time spent looking into this, there is clearly some very useful tools available.  Each one is designed with a specific use-case in mind and would be not be effective with the broad range of content / formats we would need to assess ‘out the box’.  However, their open-source nature would allow us to adjust the source code to better meet our needs - for example, removing the 2 minute limit of Chromaprint.  I think with more research and the appropriate implementation, audio fingerprinting could prove to be a very efficient method for locating duplicated content.
