### Introduction

{:.stu-note}
This is new content for the STU 2 ballot. 

The operation is being proposed as a generic export mechanism for multiple DaVinci use cases. Each use case will  define the specific content to be exported using the export operation. The atr-export operation is being defined to allow the flexibility to DaVinci use cases to specify the type of content that needs to be exported. The existing $export in the Bulk Data IG limits the exporting of data to the Patient Compartment and a server implementing $export cannot change the content being returned for each use case unless the variations are specified in the Bulk Data export parameters. 

Each DaVinci use case as part of its implementation guide can define the exportType parameter and the behavior expected.
For Member Attribution List (ATR) IG, this is specified in the [atr-export requirements](spec.html#requirements-for-implementation-of-the-atr-export-operation). 
