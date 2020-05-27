
![British Library Logo](./assets/BL_Logo_RGB_100pixels_high.jpg)
# Save our Sounds – Unlocking our Sound Heritage
 ### Absolute Time In Pregroove and CD-R id research
_April 22nd 2020_
Tom Ruane
tom.ruane@bl.uk



### Background  

For the Glastonbury New Bands collection CD-Rs were identified and matched to their ripped files using a CDDB ID (see below for details), which is a standard ID that can be generated locally using TOC data from a disc. The problem with this system, though efficient, is the number of variables used to generate the ID are limited and result in duplicate numbers across discs.

In response to this I looked at other data written to a CD-R that might be used as a more robust way to uniquely identify discs across different hardware/software tools, and aid automation and batch processing e.g. file renaming.

  

### Absolute Time in Pregroove (ATIP)

A CD-R is manufactured with a pre-groove that is used to guide the writing laser in an optical drive. The groove is written with timecode along the spiral that informs the drive of the disc’s maximum writing capacity (74 mins / 80 mins etc.); this is known as the ATIP.

  

### cdrtools

Using the opensource cdrtools suite of programmes we can interrogate a disc’s ATIP, along with other useful information.

  

Using cdrecord to read the ATIP we get the following output:

  

    cdrecord -atip dev=1,0,0
    
      
    
    ATIP info from disk:
    
    Indicated writing power: 4
    
    Disk Is not unrestricted
    
    Disk Is not erasable
    
    Disk sub type: Medium Type A, high Beta category (A+) (3)
    
    ATIP start of lead in: -11849 (97:24/01)
    
    ATIP start of lead out: 336077 (74:43/02)
    
    Disk type:  Long strategy type (Cyanine, AZO or similar)
    
    Manuf. index: 25
    
    Manufacturer: Taiyo Yuden Company Limited
    
      
    
    Capacity Blklen/Sparesz. Format-type Type
    
    228854 2048 0x00 Formatted Media

  

Here we have information on the disc manufacturer, the dye type and the ATIP.

  

The output of -atip command also includes the total number of data blocks written to the disc.

  

So The ATIP itself is not a useful indicator as the maximum values are limited (74 / 80 etc.). However, the total number of blocks used to write the data could be appended to another value (such as the CDDB ID) to add further variables and potentially reduce the likelihood of duplicated IDs.

  
  

For info - number of blocks in MBs:

  

    Capacity: 228854 Blocks = 457708 kBytes = 446 MBytes = 468 prMB
    
    Sectorsize: 2048 Bytes

  
  
  
### CDDB ID & CDINDEX

There are two common standards for IDing compact discs - CDDB ID and CDINDEX. Both systems serve the same function, to ID a disc based on information in the TOC to match up with metadata on a remote server (such as artist, album etc.)

  

The CDDB ID can be generated locally but the database it queries for commercial releases is licenced by Gracenote. The ID is generated in the following way:

  

CDDB identifies CDs with a 32-bit number, usually displayed as a hexadecimal number containing 8 digits: XXYYYYZZ. The first two digits (labeled XX) represent a checksum based on the starting times of each track on the CD. The next four digits (YYYY) represent the total time of the CD in seconds from the start of the first track to the end of the last track. The last two digits (ZZ) represent the number of tracks on the CD.

(from wikipedia)

  

The CDINDEX serves the same purpose as the CDDB ID and is generated in a similar fashion, but is free to use and was developed by MusicBrainz as an open source alternative to Gracenote.

  

Information on how the index is generated, including code samples, can be found here:

[https://musicbrainz.org/doc/Disc_ID_Calculation](https://musicbrainz.org/doc/Disc_ID_Calculation)

  

Using cdrtools we can generate the CDDB ID and CDINDEX ourselves:

  

    cdda2wav dev=1,0,0 -info-only
    
      
    
    CDINDEX discid: h5wO_6wce7emeNLLldL0PUmBTWU-
    
    CDDB discid: 0x770beb0a

  

_*not complete output of -info-only command_

  

As all the calculations are based on the data in the TOC (track number and times etc.), the variables in both cases are limited. Even though the MusicBrainz number is longer (and in theory more robust), it is really just a sha1 hash generated from the TOC data.

  

### MD5 hash

Checksums can easily be generated for Read-Only-Media such as compact discs; using standard unix/command line tools:

  

    MD5 (/dev/disk1) = 962c4a649fbdf8e315dc4df788df01de

  

This is likely to be the most unique ID we can create - however, in practical terms it takes quite long to generate, and if the data changes due to the disc degrading the hash will not match, so this isn’t likely to be a reliable option in the long term.

  

### Conclusion

Based on this research there appears to be very limited additional information written to a CDDA CD-R (other than the actual content data) that we can use to identify a disc.

  

A checksum is likely the most unique ID we can generate but as discussed above, it is not a reliable option. CDDB and CDINDEX likely use the TOC as the source input as it is not affected by data corruption in the bit stream, the possibility of duplicates is probably an accepted trade-off against maximum readability. As the matches are typically made against commercial sources mistakes are also easily identifiable and amended.

  

The simplest option going forward would be to append the CDDB ID with some of the limited data available, such as the total data blocks, disc manufacturer, and hash that into a unique ID. No off the shelf CD ripping tools offer any options like this so it would require the development of some bespoke tools/scripts.

  

### Possible further research:

Acoustic ID - [https://acoustid.org/](https://acoustid.org/)

Open source tool used to create a sonic “fingerprint” of an audio signal for matching (similat to apps like shazam).

  

Write creation date - [https://superuser.com/questions/559031/how-to-find-out-when-a-disc-dvd-has-been-written-burned](https://superuser.com/questions/559031/how-to-find-out-when-a-disc-dvd-has-been-written-burned)

The directory structure used to write data files to optical media includes a creation date - is this something that is possible to interrogate on CDDA?

  

Some way of OCR scanning the physical matrix printed on the disc?
