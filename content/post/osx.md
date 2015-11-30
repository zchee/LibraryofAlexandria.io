+++
categories = ["osx"]
date = "2015-12-01T00:46:32+09:00"
title = "OS X Darwin Kernel Resources"

+++
The OS X Darwin Kernel Resources Collection.  
Basically, link to Apple's "Mac Developer Library" references or guides.


## Performance

### Energy Efficiency and the User Experience
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Conceptual/power_efficiency_guidelines_osx

#### Related Documents
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Conceptual/power_efficiency_guidelines_osx/RelatedDocuments.html

#### Related WWDC Videos
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Conceptual/power_efficiency_guidelines_osx/WWDCVideos.html

### Table 7-1Obtaining event notifications for system services in Minimize I/O
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Conceptual/power_efficiency_guidelines_osx/Timers.html

### Performance Overview
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Conceptual/PerformanceOverview/Introduction
- Developing for Performance
- Basic Performance Tips
- Performance Tools
- Doing an Initial Performance Evaluation

### Guide: Tips in File System Programming Guide
https://developer.apple.com/library/prerelease/mac/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/PerformanceTips/PerformanceTips.html

### Data Compression
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Reference/Compression

The libcompression library provides an two API.  

#### Block compression
where all of the input data is compressed or decompressed by one call to the compression or decompression function.

#### Streaming compression
where the compression or decompression function is called repeatedly to compress or decompress data from a source buffer to a destination buffer.  
Between calls, processed data is moved out of the destination buffer and new data is loaded into the source buffer.


## XPC Services - Interprocess messages
The XPC Services API provides a low-level (libSystem) interprocess communication mechanism based on serialized property lists.

### Reference: XPC Services - API Reference
https://developer.apple.com/library/prerelease/mac/documentation/System/Reference/XPCServicesFW

### Reference: XPC Services - xpc.h
https://developer.apple.com/library/prerelease/mac/documentation/System/Reference/xpc_header_reference

### Reference: XPC Services - connection.h
https://developer.apple.com/library/prerelease/mac/documentation/System/Reference/XPC_connection_header_reference

### Reference: XPC Services - activity.h
https://developer.apple.com/library/prerelease/mac/documentation/System/Reference/activity_header_reference

### Guide: XPC - Creating XPC Service: 
https://developer.apple.com/library/prerelease/mac/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingXPCServices.html

### Guide: XPC, GCD - Manage Tasks with CTS and GCD
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Conceptual/power_efficiency_guidelines_osx/DiscretionaryTasks.html

### Guide: XPC - Defer Tasks with XPC Activity
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Conceptual/power_efficiency_guidelines_osx/CentralizedTaskScheduling.html

### XPC debugging with Xcode
https://developer.apple.com/videos/play/wwdc2013-407/
http://devstreaming.apple.com/videos/wwdc/2013/407xdx3xw3kl5xx1h5cs73sp/407/407.pdf


## Grand Central Dispatch (GCD or dispatch)
Grand Central Dispatch (GCD) comprises language features, runtime libraries, and system enhancements that provide systemic,  
comprehensive improvements to the support for concurrent code execution on multicore hardware in iOS and OS X.

### Guide: XPC, GCD - Manage Tasks with CTS and GCD
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Conceptual/power_efficiency_guidelines_osx/DiscretionaryTasks.html

### Reference: DarwinNotify - Darwin Notification API Reference
https://developer.apple.com/library/prerelease/mac/documentation/Darwin/Reference/DarwinNotify

### Guide: FSEvents: - Using the File System Events API
https://developer.apple.com/library/prerelease/mac/documentation/Darwin/Conceptual/FSEvents_ProgGuide/Introduction/Introduction.html

### Guide: Kernel Queues(kqueue) An Alternative to FSEvents (File System Events)
https://developer.apple.com/library/prerelease/mac/documentation/Darwin/Conceptual/FSEvents_ProgGuide/KernelQueues/KernelQueues.html

#### Choosing an Event Mechanism

File system events are intended to provide notification of changes with directory-level granularity.  
For most purposes, this is sufficient. In some cases, however, you may need to receive notifications with finer granularity.  
For example, you might need to monitor only changes made to a single file.  
For that purpose, the kernel queue (kqueue) notification system is more appropriate.

If you are monitoring a large hierarchy of content,  
you should use file system events instead, however, because kernel queues are somewhat more complex than kernel events,  
and can be more resource intensive because of the additional user-kernel communication involved.

### Kernel Queue and Events
http://people.freebsd.org/~jmg/kq.html

## Threading, Concurrency, Asynchronous, Parallelization

### Quelity of Service Classes (QoS)
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Conceptual/power_efficiency_guidelines_osx/PrioritizeWorkAtTheTaskLevel.html

### Reference: CFRunLoop Reference
https://developer.apple.com/library/prerelease/mac/documentation/CoreFoundation/Reference/CFRunLoopRef
A CFRunLoop object monitors sources of input to a task and dispatches control when they become ready for processing.


## Application, cli, tools

### Xcode Essentials
https://developer.apple.com/library/prerelease/mac/documentation/ToolsLanguages/Conceptual/Xcode_Overview

### Instruments User Guide
https://developer.apple.com/library/prerelease/mac/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide

### Performance Tools
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Conceptual/PerformanceOverview/PerformanceTools/PerformanceTools.html

### spindump - Profile entire system during a time interval
https://developer.apple.com/library/prerelease/mac/documentation/Darwin/Reference/ManPages/man8/spindump.8.html
Use the spindump tool with the -timeline option to sample and profile your app in order to determine which QoS class  
applies as a specific portion of code executes at a given time.

```
$ sudo spindump -timeline ListerOSX
 
Thread 0x48e64c     1000 samples (1-1000) priority 37
<thread QoS user initiated, IO policy standard>
1000  thread_start + 13 (libsystem_pthread.dylib + 5149) [0x7fff8c3aa41d] 1-1000
  1000  _pthread_start + 176 (libsystem_pthread.dylib + 12773) [0x7fff8c3ac1e5] 1-1000
      1000  _pthread_body + 131 (libsystem_pthread.dylib + 12904) [0x7fff8c3ac268] 1-1000
```

### powermetrics - gathers and display CPU usage statistics
Use the powermetrics tool to analyze your app and determine how much time is being allocated to different QoS classes.
https://developer.apple.com/library/prerelease/mac/documentation/Darwin/Reference/ManPages/man1/powermetrics.1.html

```
$ sudo powermetrics --show-process-qos --samplers tasks
*** Sampled system activity (Fri Feb 20 11:55:48 2015 -0800) (5004.56ms elapsed) ***
 
*** Running tasks ***
 
Name   ID   CPU ms/s   User%   Deadlines   (<2 ms, 2-5 ms)   Wakeups (Intr, Pkg idle)   QOS (ms/s)   Default   Maint   BG   Util   Lgcy   U-Init   U-Intr
ListerOSX   8083   21.05   79.16   0.00   0.00   10.19   4.60   0.00   0.00   0.00   0.00   0.43   0.62   19.96>)
```

### top - display and update sorted information about processes
https://developer.apple.com/library/prerelease/mac/documentation/Darwin/Reference/ManPages/man1/top.1.html

### timerfires -- analyze timers as they fire
https://developer.apple.com/library/prerelease/mac/documentation/Darwin/Reference/ManPages/man1/timerfires.1.html

### sample -- Profile a process during a time interval
https://developer.apple.com/library/prerelease/mac/documentation/Darwin/Reference/ManPages/man1/sample.1.html

### pmset -- manipulate power management settings
https://developer.apple.com/library/prerelease/mac/documentation/Darwin/Reference/ManPages/man1/pmset.1.html

### fs_usage -- report system calls and page faults related to filesystem activity in real-time
https://developer.apple.com/library/prerelease/mac/documentation/Darwin/Reference/ManPages/man1/fs_usage.1.html

### sc_usage -- show system call usage statistics
https://developer.apple.com/library/prerelease/mac/documentation/Darwin/Reference/ManPages/man1/sc_usage.1.html

### dtrace - generic front-end to the DTrace facility
https://developer.apple.com/library/prerelease/mac/documentation/Darwin/Reference/ManPages/man1/dtrace.1.html


## Misc

### Apple Developer Library 日本語ドキュメント
https://developer.apple.com/jp/documentation/

### Reference: notifications - NSNotificationnCenter
https://developer.apple.com/library/prerelease/mac/documentation/Cocoa/Reference/Foundation/Classes/NSNotificationCenter_Class

### Blocks Programming Topics
https://developer.apple.com/library/prerelease/mac/documentation/Cocoa/Conceptual/Blocks/Articles/00_Introduction.html
Block objects are a C-level syntactic and runtime feature.

### OpenCL
https://developer.apple.com/library/prerelease/mac/technotes/tn2335/_index.html

# Apple's Mac Developer Library Sample Code

## Earthquakes
Populating a Core Data Store Using a Background Queue.

| Last Revision           | Build Requirements        | Runtime Requirements |
|-------------------------|---------------------------|----------------------|
| Version 1.3, 2015-10-21 | Xcode 7.0, OS X 10.11 SDK | OS X 10.9            |

https://developer.apple.com/library/prerelease/mac/samplecode/Earthquakes/Introduction/Intro.html
Download Sample Code: https://developer.apple.com/library/prerelease/mac/samplecode/Earthquakes/EarthquakesPopulatingaCoreDataStoreUsingaBackgroundQueue.zip

## DeferredShaing
In deferred shading, no shading is performed in the first pass of the vertex and pixel shaders.  

| Last Revision           | Build Requirements      | Runtime Requirements |
|-------------------------|-------------------------|----------------------|
| Version 2.0, 2015-07-08 | OS X 10.10 SDK or later | OS X 10.8 or later   |

Revision: Updated to OpenGL Core Profile, Xcode 10.10 SDK

https://developer.apple.com/library/prerelease/mac/samplecode/DeferredShading/Introduction/Intro.html  
https://developer.apple.com/library/prerelease/mac/samplecode/DeferredShading/DeferredShading.zip

## CloudSearch
How to find documents in iCloud, using NSMetaDataQuery.

| Last Revision           | Build Requirements               | Runtime Requirements           |
|-------------------------|----------------------------------|--------------------------------|
| Version 2.0, 2015-05-18 | iOS 8.0, OS X 10.10 SDK or later | iOS 8.0, OS X 10.9 or later    |

https://developer.apple.com/library/prerelease/mac/samplecode/CloudSearch/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/CloudSearch/CloudSearch.zip

## Unit Testing Apps and Frameworks
Shows how to build a static library for an iOS app and a Mac app.

| Last Revision           | Build Requirements                       | Runtime Requirements           |
|-------------------------|------------------------------------------|--------------------------------|
| Version 1.2, 2014-09-29 | Xcode 5, iOS 7.0, OS X 10.8 SDK or later | iOS 7.0, OS X 10.8 or later    |

https://developer.apple.com/library/prerelease/mac/samplecode/UnitTests/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/UnitTests/UnitTests.zip

## enetlognke
`enetlognke` is an NKE (network kernel extension) that demonstrates the interface filter KPI (kernel programming interface).

| Last Revision           | Build Requirements | Runtime Requirements |
|-------------------------|--------------------|----------------------|
| Version 2.0, 2014-05-12 | Xcode 5.1          | OS X 10.9 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/enetlognke/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/enetlognke/enetlognke.zip

## KauthORama
KauthORama demonstrates the use of the Kernel Authorization (Kauth) subsystem.

| Last Revision           | Build Requirements | Runtime Requirements |
|-------------------------|--------------------|----------------------|
| Version 1.4, 2014-03-26 | Xcode 5.1          | OS X 10.9 or later   |

## PreLoginAgents
