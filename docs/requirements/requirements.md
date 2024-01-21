# Requirements

## Scope or Objective
Design and build an application that can search documents
from a cloud storage service like Dropbox or Google Drive
on the content inside the document.

## Personas
* Administrator: One who will configure the file read service.
* End User: The user of the search service.

**Note:** Administrator will also look after the pipeline.

## Functional Requirements
* Connect to storage devices such as Google Drive, Dropbox or S3.
* Fetch the files hosted on the storage.
* The files can be utf-8 encoded or may also have other non-utf-8 characters.
* The files can be of any of the following types: txt, csv, pdf, .docx.
* Utilize the elasticsearch with index facility to allow for searching files.
* Search can also be on the metadata of the file.
* Expose an API that can perform the search operation and return the file with the path.
* An explicit query string is required if the search is based on the file's metadata instead of the content.
* Build a CLI that can return the response and print the outcome.

## Non-functional Requirements
* Scalability:
  * The solution may connect to multiple data sources.
  * The files stored on the external storage may be of any arbitrary
    length.
  * The search solution (elasticsearch) is horizontally scalable or
    has an option to shard and store for scaling on the increasing
    data needs.
* Availability:
  * The search service is highly available.
  * Once the file is consumed from the storage service it is available
    for the search.
* Throughput/Latency/Performance:
  * Files are processed in batches. There may be delay from the time
    a file is added to the storage service before it is available
    in the search service.
  * However, once the search service is aware of the data, it responds
    to the query much faster.
* Data Standards:
  * All the files are assumed to convert to UTF-8 before search is
    performed.
* Security:
  * Please check the assumptions section for the data encryption/privacy
    related considerations.
  * The query service endpoint is protected with TLS and is enabled
    with authentication.
* Observability:
  * Have an option to trace and track each request.
  * Track metrics across services to identify bottlenecks.
  * Monitor logs for any error statements.

## Assumptions
* The file sizes can be read at once, a large arbitrary file sizes
  are supported in later iterative releases.
* The files can be nested inside a folder on the storage drive.
* The connection parameters are statically configured by the 
  administrator.
* A newly added file is not immediately available for the search API.
* A search query can be a string and it cannot be a map or an object.
  For example, in case of a CSV file, one cannot expect a column name
  to search for the contents under the column.
* The data is assumed to the compliant to store in plain text and no
  special security measures are considered. If there are privacy
  preserving needs then additional measures are required.
* The administrator is assumed to be configuring with the authentication
  and/or optional authorizing credentials to access the external storage.
* The runtime environment is expected to capture logs for future
  processing.
* The cost factor for indexing entire file/directory structure may be
  higher as the size grows. The cost factor is not considered in
  designing the solution.
* The query service authentication/authorization is implemented in simple
  manner for the demo purpose, a detailed deployment walk through
  is needed before the production release.
