### Introduction

{:.stu-note}
This is new content for the STU 2 ballot. 

This operation is a profiled version of the [Bulk Data Export Operation]({{site.data.fhir.ver.bulkig}}/index.html)). The parameters defined in the base Bulk Data Export operation are reused in this specification.

The operation is being proposed as a generic export mechanism for multiple DaVinci use cases. Each use case will  define the specific content to be exported using the export operation. The davinci-data-export operation is being defined to allow the flexibility to DaVinci use cases to specify the type of content that needs to be exported. The existing $export in the Bulk Data IG limits the exporting of data to the Patient Compartment and a server implementing $export cannot change the content being returned for each use case unless the variations are specified in the Bulk Data export parameters. 
Similar to any FHIR operation, Consumers need to obtain authorization to successfully invoke the operation. 

Each DaVinci use case as part of its implementation guide can define the exportType parameter and the behavior expected.
For Member Attribution List (ATR) IG, this is specified in the [davinci-data-export requirements](spec.html#requirements-for-implementation-of-the-davinci-data-export-operation). 

Producers **SHALL** return values from the operation as per the [FHIR Operation Response Specification](https://hl7.org/fhir/operations.html#response)