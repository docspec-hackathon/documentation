# Document conversion reporting format (DRCF)

(Note this document is work-in-progress)

## Goal
When converting a document from a different markup/syntax into another one, a conversion might not always allow to retain all data. This document specifies a JSON-based report format for conversion tools to keep track of conversion issues.

The report format might be used for various purposes such as:
- Generate to pre-migration report of potential issue
- Show document-specific issues in the Docs UI or attach as a record

## Data structure
Document conversion issues are JSON objects. We propose the following properties:
- id: int (report element id)
- severity: INFO, WARNING, ERROR
- scope: DOCUMENT, BLOCK (more...)
- action: STRUCTURAL_CHANGE (more...) (conversion action applied)
- side: SOURCE, DATA, DESTINATION, TOOL (origin of issue; optional)
- action_code: int (action/issue code for looking up in documentation)
- message: String (issue/error message string; optional)
- source_uri: String (URI/path of the source)
- destination_uri: String (URI/path of the destination; optional)
- source_line: int (source line of code related to the issue; optional)
- source_reference: String (source identifier related to the issue; optional)
- source_raw: String (raw data; for debugging purposes; optional)
- destination_line: int (destination line of code related to the issue; optional)
- destination_reference: String (destination identifier related to the issue; optional)

## Example
```
[{
	"id" : 1,
	"source_uri": "file://myDoc1.docx",
	"destination_uri": "https://localhost/docs/doc1",
	"severity": "WARNING",
	"scope": "BLOCK",
	"action": "STRUCTURAL_CHANGE",
	"action_code": 123,
	"source_reference": "block1",
	"destination_reference": "block1"
},
{
	"id" : 2,
	"source_uri": "file://myDoc2.docx",
	"destination_uri": "https://localhost/docs/doc1",
	"severity": "ERROR",
	"scope": "BLOCK",
	"action": "SKIPPED",
	"action_code": 129,
	"message": "Block type 'table' not supported by destination",
	"source_reference": "block1",
},
{
	"id": 3,
	"source_uri": "file://myDoc3.docx",
	"severity": "ERROR",
	"scope": "DOCUMENT",
	"action": "SKIPPED",
	"action_code": 125,
}]
```

## List
The following list is a (work in progress) list to collect types of conversion issuss, which could be represented in the format above. Issues below likely would be assigned an "action_code" id.

### External (beyond document scope)
- Document hierarchy not supported
- Document reference can't be resolved
- Document inclusion not supported
- Document metadata not supported
- Document attachment not supported
- Document history not supported
- ACL not supported
- ...

### Internal (within document scope)
- General document parse error (protected, broken)
- Block hierarchy not supported
- Images not supported
- Tables not supported
- Comments not supported
- ...
