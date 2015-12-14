+++
categories = ["osx"]
date = "2015-12-01T00:46:32+09:00"
title = "OS X Darwin Kernel Resources"

+++
The OS X Darwin Kernel Resources Collection.  


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

### Reference: Grand Central Dispatch (GCD) Reference
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Reference/GCD_libdispatch_Ref/index.html

### Guide: XPC, GCD - Manage Tasks with CTS and GCD
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Conceptual/power_efficiency_guidelines_osx/DiscretionaryTasks.html

### Guide: Prioritize Work at the Task Level
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Conceptual/power_efficiency_guidelines_osx/PrioritizeWorkAtTheTaskLevel.html

## Kernel Events

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

### Concurrency Programming Guide
Concurrency is the notion of multiple things happening at the same time.
https://developer.apple.com/library/prerelease/mac/documentation/General/Conceptual/ConcurrencyProgrammingGuide

### Threading Programming Guide
Threads are one of several technologies that make it possible to execute multiple code paths concurrently inside a single application.
https://developer.apple.com/library/prerelease/mac/documentation/Cocoa/Conceptual/Multithreading

### Quelity of Service Classes (QoS)
https://developer.apple.com/library/prerelease/mac/documentation/Performance/Conceptual/power_efficiency_guidelines_osx/PrioritizeWorkAtTheTaskLevel.html

### Reference: CFRunLoop Reference
https://developer.apple.com/library/prerelease/mac/documentation/CoreFoundation/Reference/CFRunLoopRef
A CFRunLoop object monitors sources of input to a task and dispatches control when they become ready for processing.


## Application, cli, tools

### Xcode Essentials
https://developer.apple.com/library/prerelease/mac/documentation/ToolsLanguages/Conceptual/Xcode_Overview

### Xcode Server API
https://developer.apple.com/library/prerelease/mac/documentation/Xcode/Conceptual/XcodeServerAPIReference

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

### Reference: notifications center - NSNotificationnCenter
https://developer.apple.com/library/prerelease/mac/documentation/Cocoa/Reference/Foundation/Classes/NSNotificationCenter_Class

### System Integrity Protection(SIP) Guide
https://developer.apple.com/library/prerelease/mac/documentation/Security/Conceptual/System_Integrity_Protection_Guide/Introduction/Introduction.html

### Blocks Programming Topics
https://developer.apple.com/library/prerelease/mac/documentation/Cocoa/Conceptual/Blocks/Articles/00_Introduction.html
Block objects are a C-level syntactic and runtime feature.

### OpenCL
https://developer.apple.com/library/prerelease/mac/technotes/tn2335/_index.html

### Configuration Profile Key Reference
https://developer.apple.com/library/prerelease/mac/featuredarticles/iPhoneConfigurationProfileRef/Introduction/Introduction.html


# Apple's Mac Developer Library Sample Code

## SignalProcessing
Using Biquadratic Filter Functions

| Last Revision           | Build Requirements     | Runtime Requirements |
|-------------------------|------------------------|----------------------|
| Version 1.0, 2015-10-21 | Xcode 7.0, iOS 9.0 SDK | iOS 9.0              |

https://developer.apple.com/library/prerelease/mac/samplecode/SignalProcessing/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/SignalProcessing/SignalProcessingUsingBiquadraticFilterFunctions.zip

## CompressionSample
Compressing Blocks and Streams of Data

| Last Revision           | Build Requirements        | Runtime Requirements |
|-------------------------|---------------------------|----------------------|
| Version 1.0, 2015-10-21 | Xcode 7.0, OS X 10.11 SDK | OS X 10.11           |

https://developer.apple.com/library/prerelease/mac/samplecode/CompressionSample/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/CompressionSample/CompressionSampleCompressingBlocksandStreamsofData.zip

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
Compressing Blocks and Streams of Data

| Last Revision           | Build Requirements | Runtime Requirements |
|-------------------------|--------------------|----------------------|
| Version 1.1, 2014-04-07 | Xcode 5.1          | OS X 10.9            |

https://developer.apple.com/library/prerelease/mac/samplecode/PreLoginAgents/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/PreLoginAgents/PreLoginAgents.zip

## Performing Serial I/O
Command line tool that demonstrates how to use IOKitLib to find all serial ports on OS X.

| Last Revision           | Build Requirements     | Runtime Requirements |
|-------------------------|------------------------|----------------------|
| Version 1.5, 2013-11-07 | Os X 10.6 SDK or later | OS X 10.6 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/SerialPortSample/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/SerialPortSample/SerialPortSample.zip

## SMJobBless
SMJobBless demonstrates how to securely install a helper tool that performs a privileged operation and  
how to associate the tool with an application that invokes it.

| Last Revision           | Build Requirements | Runtime Requirements |
|-------------------------|--------------------|----------------------|
| Version 1.5, 2013-09-17 | Xcode 4.6 or later | OS X 10.6 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/SMJobBless/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/PreLoginAgents/PreLoginAgents.zip

## SampleUSBAudioOverrideDriver
This project demonstrates how to override certain properties of a USB audio device using a codeless kernel extension (kext).

| Last Revision           | Build Requirements                           | Runtime Requirements |
|-------------------------|----------------------------------------------|----------------------|
| Version 1.2, 2013-06-03 | Xcode 5.4.2 or later, Mac OS X 10.8 or later | OS X 10.7 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/SampleUSBAudioOverrideDriver/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/SampleUSBAudioOverrideDriver/SampleUSBAudioOverrideDriver.zip

## NotifyTool
NotifyTool is a simple example of how to use the BSD notify API (man 3 notify).

| Last Revision           | Build Requirements | Runtime Requirements |
|-------------------------|--------------------|----------------------|
| Version 1.1, 2012-08-19 | Xcode 4.4          | OS X 10.6            |

https://developer.apple.com/library/prerelease/mac/samplecode/NotifyTool/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/NotifyTool/NotifyTool.zip

## Sandboxing with NSXPCConnection
"SandboxingAndNSXPCConnection" shows how the security concept of least privilege separation  
can be implemented using App Sandboxing and XPC interprocess communication (IPC).

| Last Revision           | Build Requirements                     | Runtime Requirements |
|-------------------------|----------------------------------------|----------------------|
| Version 1.0, 2012-08-21 | Xcode 4.4 or later, OS X 10.8 or later | OS X 10.8 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/SandboxingAndNSXPCConnection/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/SandboxingAndNSXPCConnection/SandboxingAndNSXPCConnection.zip

## ClipboardViewer
This small application shows the contents of any clipboard.

| Last Revision           | Build Requirements                     | Runtime Requirements |
|-------------------------|----------------------------------------|----------------------|
| Version 1.2, 2012-06-07 | Xcode 4.0 or later, OS X 10.7 or later | OS X 10.7 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/ClipboardViewer/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/ClipboardViewer/ClipboardViewer.zip

## Cache
NSCache demonstration, also using NSImage, NSView, NSTimer, and NSBitmapImageRep.

| Last Revision           | Build Requirements                     | Runtime Requirements |
|-------------------------|----------------------------------------|----------------------|
| Version 1.0, 2012-05-30 | Xcode 4.0 or later, OS X 10.7 or later | OS X 10.7 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/Cache/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/Cache/Cache.zip

## Core Data Utility
This sample contains the complete source code to the Core Data Utility Tutorial.

| Last Revision           | Build Requirements | Runtime Requirements |
|-------------------------|--------------------|----------------------|
| Version 1.0, 2012-04-04 | Xcode 4.4 or later | OS X 10.8 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/CoreDataUtility/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/CoreDataUtility/CoreDataUtility.zip

## Dispatch_Compared
This sample code measures the performance of invoking and executing various parallel APIs, in comparison to serial equivalents a simple for loop,  
GCD: dispatch_apply,  
GCD: serial queue,  
GCD: parallel queue,  
GCD: multiple queues,  
OpenMP, and POSIX threads.

| Last Revision           | Build Requirements | Runtime Requirements |
|-------------------------|--------------------|----------------------|
| Version 1.0, 2009-09-08 | OS X 10.6 or later | OS X 10.6 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/Dispatch_Compared/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/Dispatch_Compared/Dispatch_Compared.zip

## DispatchFractal
Shows how to combine parallel computation of fractals on the CPU via GCD with results processing and display on the GPU via OpenCL and OpenGL.

| Last Revision           | Build Requirements | Runtime Requirements |
|-------------------------|--------------------|----------------------|
| Version 1.0, 2009-06-05 | OS X 10.6 or later | OS X 10.6 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/DispatchFractal/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/DispatchFractal/DispatchFractal.zip

## DispatchLife
The classic game of Life showing use of dispatch queues as lightweight threads (each cell is a queue),  
and an example of how to avoid overloading a slow queue (OpenGL or curses screen updates) with many requests (cell updates)  
by using a timer to drive the screen updates and allowing the cells to update as fast as they can.

| Last Revision           | Build Requirements | Runtime Requirements |
|-------------------------|--------------------|----------------------|
| Version 1.2, 2009-05-29 | OS X 10.6 or later | OS X 10.6 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/DispatchLife/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/DispatchLife/DispatchLife.zip

## Dispatch_Samples
Examples of using Grand Central Dispatch (GCD) sources (file, network, and timers), dispatch_apply,dispatch_group.

| Last Revision           | Build Requirements | Runtime Requirements |
|-------------------------|--------------------|----------------------|
| Version 1.0, 2009-05-29 | OS X 10.6 or later | OS X 10.6 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/Dispatch_Samples/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/Dispatch_Samples/Dispatch_Samples.zip

## DispatchWebServer
A web server that uses one queue per HTTP connection.

| Last Revision           | Build Requirements | Runtime Requirements |
|-------------------------|--------------------|----------------------|
| Version 1.1, 2009-05-29 | OS X 10.6 or later | OS X 10.6 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/DispatchWebServer/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/DispatchWebServer/DispatchWebServer.zip

## FSMegaInfo
This tool is designed to help folks who are implementing a plug-in file system (VFS plug-ins) on Mac OS X.

| Last Revision           | Build Requirements | Runtime Requirements |
|-------------------------|--------------------|----------------------|
| Version 1.0, 2008-02-25 | Xcode 3.0          | OS X 10.4 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/FSMegaInfo/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/FSMegaInfo/FSMegaInfo.zip

## Duplicate Finder Items
This sample project shows how to build an Automator action targeting Finder using AppleScript.

| Last Revision           | Build Requirements | Runtime Requirements |
|-------------------------|--------------------|----------------------|
| Version 1.0, 2005-06-06 | Xcode 2.1          | OS X 10.4 or later   |

https://developer.apple.com/library/prerelease/mac/samplecode/DuplicateFinderItems/Introduction/Intro.html
https://developer.apple.com/library/prerelease/mac/samplecode/DuplicateFinderItems/DuplicateFinderItems.zip
