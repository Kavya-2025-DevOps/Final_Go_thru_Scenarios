
pipeline  

1. What strategies you use to reduce the pipeline execution time (40 mint -> 10 mint)
   1. Measure Before Optimizing - First, identify where the 40 minutes are being spent.  
   2. Parallelize Independent Jobs - One of the highest-impact improvements. (eg: Build → Unit Test + Integration Test + Security Scan)
   3. Implement Dependency Caching - Avoid downloading dependencies every run. (eg: Maven .m2; Gradle cache; npm cache; pip cache; Docker layers;)
   4. Docker Layer Optimization - Bad Dockerfiles often add several minutes.  
   5. Optimize Infrastructure - (eg: 2 CPU Runner - upgrade to - 8 CPU Runner)
   6. Reuse Build Artifacts - Avoid rebuilding the same code.

2. 
