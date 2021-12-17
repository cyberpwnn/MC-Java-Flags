These are some Shenandoah flags I put together with the help of [this](https://krusic22.com/2020/03/25/higher-performance-crafting-using-jdk11-and-zgc/) blogpost<br/>
Note that these flags require you to have Java 12+ though I would always suggest you to use the last Java version available

# The flags

-XX:ShenandoahAllocSpikeFactor=5 -XX:ShenandoahControlIntervalAdjustPeriod=1000 -XX:ShenandoahControlIntervalMax=10 -XX:ShenandoahControlIntervalMin=1 -XX:ShenandoahInitFreeThreshold=70 -XX:ShenandoahGarbageThreshold=25 -XX:ShenandoahGuaranteedGCInterval=300000 -XX:ShenandoahMinFreeThreshold=10 -XX:-ShenandoahRegionSampling -XX:ShenandoahRegionSamplingRate=40

# Explaining some of these flags 

+UnlockExperimentalVMOptions – Unlocks experimental flags/options,
+DisableExplicitGC – Disables System.gc() calls from code, you really don’t want people playing around with your GC,
-UseParallelGC – Disables Parallel GC, this should already be disabled, but we set this just to be sure,
-UseParallelOldGC – ^ but disables ParalledOld GC,
-UseG1GC – ^ but disables G1GC,
+AlwaysPreTouch – AlwaysPreTouch gets the memory setup and reserved at process start ensuring it is contiguous, improving the efficiency of it more. This improves the operating systems memory access speed. Mandatory to use Transparent Huge Pages,
+ParallelRefProcEnabled – Optimizes the GC process to use multiple threads for weak reference checking,


