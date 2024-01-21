# Product and Engineering Requirements Document

The document outlines the detailed task level information.
The task break down is done considering a agile development
model. An incremental release cycle will be followed to facilitate
iterative demo.

These tasks are created based on the design defined at
[High Level Design](../design/hld.md) document.

## Alpha Release (MVP):

Scope: Demo a solution that can read stored files, index them and
extend the search capability.

| Epic                             | Task                                                                                    |
|----------------------------------|-----------------------------------------------------------------------------------------|
| Read Text File From Google Drive | Authenticate and connect to Google Drive.                                               |
|                                  | Authorize and read files from the specified directory.                                  |
|                                  | Read every file which is txt extension, iteratively include any subfolders too.         |
|                                  | Ingest files as they exist on the Google drive.                                         |
| Query Service for User Searches  | Scalable service to connect with elasticsearch and perform the search on user query     |
| | The API is enabled with the siple secret based authentication                           |
| Develop a User friendly CLI      | Use simple bash script to utilize the available commands such as CURL to make API call. |
|                                  | Pretty print the API response for user readability.                                     |
| Demo Setup                       | Create a container environment where all services are run in one docker-compose file.   |
|                                  | Generate test directory and perform the demo as expected in the requirements.           |

## Beta Release (MVP+):

Scope:
1. Include non UTF-8 character files.
2. Allow for dynamic file changes to reflect the system.

| Epic | Task                                                                                       |
|--- |--------------------------------------------------------------------------------------------|
| Support for non UTF-8 files | Introduce the library to read files and encode them to string                              |
| Dynamic file change | Listen to the storage directory changes or add a scheduler to check at a regular frequency |
| | Upon a change detection, remove the indexing associated with the file that is deleted.     |
| | Upon addition of a new file, introduce new indexes for the new file.                       |

## Release 1.0 (MVP++):

Scope:
1. Include additional file types for indexing and searching.
2. Make the file read a highly available service, so that dynamic
   file change mechanism is robust and reliable.

| Epic | Task                                                          |
|--- |---------------------------------------------------------------|
| Support additional file types | Parse the files with an extension such as .docx, .csv or .pdf |

## Future Release Plans
* Support for large file reads.
* Support additional storage drives such as S3, Dropbox in addition to Google Drive.
* Introduce additional caching layers as needed.
* Protect the API endpoint with the TLS parameter.
* Introduce a deployment strategy for effortless scaling.
* Introduce logging and monitoring mechanism for identifying issues.
* Track metrics across services.
* Support existing ETL tool integrations for on-demand deployment.

## Next

1. Check the [HLD](./../design/hld.md).
2. Go back to project's [readme.md](../../readme.md)
