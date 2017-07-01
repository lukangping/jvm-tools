Swiss Java Knife
=========
[![Build Status](https://travis-ci.org/aragozin/jvm-tools.png?branch=master)](https://travis-ci.org/aragozin/jvm-tools)

SJK is a command line tool for JVM diagnostic, troubleshooting and profiling.

SJK exploits standard diagnostic interfaces of JVM (such as JMX, JVM attach and perf counters) and add some more logic on top 
to be useful for common troubleshooting case.


Prebuild binaries for version 0.6 are below
- [sjk.jar - all commands without mxdump](https://repo1.maven.org/maven2/org/gridkit/jvmtool/sjk/0.6/sjk-0.6.jar)
- [sjk-plus.jar - all commands](https://repo1.maven.org/maven2/org/gridkit/jvmtool/sjk/0.6/sjk-plus-0.6.jar)


Starting sjk
----

    java -jar sjk.jar <cmd> <arguments>
    java -jar sjk.jar --commands
    java -jar sjk.jar --help <cmd>

Below a few command from SJK ([full command reference](sjk-core/COMMANDS.md)).

[ttop]
----

Pools thread CPU usage of target JVM and periodically report to console.

 - can attach via PID or open JMX port
 - display thread memory allocation rate and cumulative process allocation rate
 - display safe point time consumption (only if attache via PID)

[More details](sjk-core/COMMANDS.md#ttop-command)

[jps]
----

Similar to `jps` from JDK. 

- plus could display specific system properties of process in output
- plus could display values of specific -XX for HotSpot JVM processes 
- plus could filter process java processes by their system properties
 
[More details](sjk-core/COMMANDS.md#jps-command)

[hh]
----

Similar to `jmap -histo`.

 - plus can show histogram of dead objects (histograms of all and live requested, then difference is calculated)
 - plus can show N top buckets in histogram

[More details](sjk-core/COMMANDS.md#hh-command)

[stcap], [stcpy] and [ssa]
----

These commands provide basic sample profiler capabilities. `stcap` produces hyper-dense stack trace dump 
(about 1000 compression rate compared to text format) and `ssa` provides few reports over dump files.
`stcpy` can copy data in archives produced by `stcap` (e.g. merging dumps or filtering selected threads).

So far following reports are available

 - [sophisticated filtering] (time, stack trace, thread name)
 - stack frame histogram with advanced filtering options
 - flame graph visualization (SVG)
 - per thread summary (CPU usage, memory allocation, etc)
 - converting back to text format

Dump file can be also processed programatically.

[More details](sjk-core/COMMANDS.md#ssa-command)

[mx]
-----

This command allow you to do basic operations with MBean from command line.

It can

 - read MBean attributes
 - update MBean writeable attributes
 - invoke MBean operations (arguments are supported)
 - displays composite and tabular data in human readable format
 - use wild cards to shorten MBean names (e.g. `*:*,name=CodeCacheManager` instead of `java.lang:type=MemoryManager,name=CodeCacheManager`)
 - connect to local JVM processes by PID (e.i. any Java process, you do not need to enable JMX server)
 - connect to JMX using host:port (password authentication is supported)

[More details](sjk-core/COMMANDS.md#mx-command)

[gc]
-----

Report information about GC in real time. Data is retrieved via JMX.

[More details](sjk-core/COMMANDS.md#gc-command)

mxdump
-----

Dumps all MBeans of target java process to JSON.

 [ttop]: sjk-core/COMMANDS.md#ttop-command
 [jps]: sjk-core/COMMANDS.md#jps-command
 [hh]: sjk-core/COMMANDS.md#hh-command
 [gc]: sjk-core/COMMANDS.md#gc-command
 [mx]: sjk-core/COMMANDS.md#mx-command
 [stcap]: sjk-core/COMMANDS.md#stcap-command
 [stcpy]: sjk-core/COMMANDS.md#stcpy-command
 [ssa]: sjk-core/COMMANDS.md#ssa-command
 [sophisticated filtering]: sjk-core/src/main/resources/org/gridkit/jvmtool/cmd/ssa-help.md
