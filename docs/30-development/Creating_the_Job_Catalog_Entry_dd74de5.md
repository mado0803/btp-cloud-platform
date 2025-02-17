<!-- copydd74de51600f49fca781cbae31130d9f -->

# Creating the Job Catalog Entry

Instead of a respective editor in ADT, *Job Catalog Entries* and *Job Templates* need to be created via a released API. This API shall be called from within a console application. The console application is only required in the development system.

Job catalog entries and job templates are created with a package assignment and the objects are assigned to a transport request. You need to make sure that the package and transport request fit together \(regarding the transport layer\) and that possible naming conventions are obeyed.

The job catalog entry mainly contains the reference to the implementation class of the business logic.

> ### Example:  
> A code example of a console application that generates the minimal number of required development objects: One job catalog entry and one related job template is shown in *Creating the Job Template* \(see *Related Links* below\).

**Related Information**  






[Scheduling an Application Job](../50-administration-and-ops/Scheduling_an_Application_Job_147d689.md "Find out how to schedule an Application Job.")

