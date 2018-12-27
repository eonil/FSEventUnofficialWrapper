ARCHIVED!
=========
This repository has been replaced by a new repository: https://github.com/eonil/FSEvents

----



FSEventsUnofficialWrapper
=============================
Hoon H.

[![Build Status](https://api.travis-ci.org/eonil/fsevents-unofficial-wrapper.svg)](https://travis-ci.org/eonil/fsevents-unofficial-wrapper)

It's possible to use FSEvents directly in Swift 3, but it still involves
many boilerplate works and subtle conversions.

This library provides mostly faithful wrapper around FSEvents feature tailored
for Swift 3.



Quickstart
----------
Import.

    import FSEventsUnofficialWrapper

Start.

    try FileSystemWatch.start(for: ObjectIdentifier(self), paths: ["/"]) { event in
        print(event)
    }

Stop.

    FileSystemWatch.stop(for: ObjectIdentifier(self))



Using Full Feature
------------------
Make a `FSEventUnofficialWrapperStream`, schedule it to a GCD queue, and start.

    let s = try FSEventUnofficialWrapperStream(pathsToWatch: paths,
                                               sinceWhen: .now,
                                               latency: 0,
                                               flags: [],
                                               handler: handler)
    s.setDispatchQueue(DispatchQueue.main)
    try s.start()

After use, deinitialize by stop, invalidate(unschedule).

    s.stop()
    s.invalidate()

As soon as the last strong reference removed, the stream will be destroyed.





License
-------
MIT license.
