# trakker
trakker is an open-source utility that helps you keep track of used space on your hard disk. Unlike most utilities of this kind, trakker tracks what has changed on the disk to help you understand sudden increases in used space.


## Vision
trakker shall be modular, so that it can be easily extended to support new file systems and devices (e.g. Windows, Linux, Android...)
Its frontend shall be portable or even web-based.

## Backend
#### File System Snapshot
A file system snapshot is a JSON document that contains information about all drives and directory trees on a certain device. 
A snapshot represents the state of the file system at a certain point in time.

#### Snapshot Generator
A snapshot generator is a stand-alone executable that will have to be re-written per file system type, but does not require a lot of logic at all.
A generator will normally run in the background and thus shall not consume a lot of CPU nor RAM.

On some file systems such as NTFS, generators will make calculations to compensate for missing data, such as the "size" field of directories.

#### Diff Generator
The diff generator is a heavier backend component, which will likely be implemented as a web service.
Given two snapshots, the diff generator is tasked with producing a JSON document that describes how the file system has changed.

If you think about this project in MVVM terms, the diff generator's product is the ViewModel and the snapshots are the models.

## Frontend
#### Diff view
This view should simplify the task of finding out the major differences in size between two snapshots, as well as reflect additions and deletions.

#### Keeping track of snapshots
Let users clean up snapshots;
Take snapshots periodically (e.g. every 3 days);

#### Polling drives
On NTFS and possibly other file systems, it is easy to track used space on all hard drives. trakker client should detect major increases in used space (compared to the used space in the latest snapshot) and trigger a snapshot.
