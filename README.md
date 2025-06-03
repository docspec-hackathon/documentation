## Introduction

Importing existing documents is a major enabling factor for the success of novel tools such as [La Suite Docs](https://github.com/suitenumerique/docs).

Due to the nature of Docs, various types of sources such as document files but also software systems such as Intranets or Wikis can be considered relevant. Microsoft Word Documents (".docx") are probably the source with the highest practical relevance.

In this hackathon project, we worked on three interrelated topics:
- Mapping an initial big picture describing ways to import data to Docs
- Implementing a PoC for the conversion of .docx files to Docs BlockNote elements, including an integration in the Docs user interface
- Drafting a specification for capturing issues encountered during conversion to help inform users.

## Migrating and importing documents to Docs

Successfully switching to Docs is not just the technical import of source documents. It is also about creating a clear understanding of the complete migration process, questions to decided on and issues to be dealt with.

Not all of the aspects discussed in the following will be relevant for each Docs user community, but it may be helpful for both potential Docs users, and also the Docs development community to understand challenges, options and limitations related to data import.

![Overview describing aspects in the migration of Documents to Docs](/assets/lasuite-docs-migration-big-picture.drawio.png)

### Data sources

We distinguish between documents as files (e.g. ".docx.", ".txt") and "documents as data structures", the latter coming from systems/APIs such as Intranets, Notion or Wikis. Documents as files may be sources from a file system or also from an API (e.g, Dropbox or SharePoint).

There may be two modes of important to consider:
- Bulk migration of an existing document base
- Ad hoc import of individual files

The bulk migration case is typically more challenging, especially in an organizational setting with various users. Even before considering import at the document level, analyzing the data source can give valuable insights for the further process:
- Gathering information about the total and individual size of data (e.g., max files sizes!)
- Gathering information about "buckets" of data, which may drive resource modeling (user folders, shared folders, ..) on the destination side

Some sort of scanning/reporting tool can be helpful in this stage already in order to inform further process planning.

### Conversion

Once higher-level topics such as "which folders to migrate where" have been addressed, it gets to conversion at the document level.  y design, Docs will never aim for a 100% feature match with Desktop Word Processing tools. Also other relevant import sources might contain certain features not available in Docs.

Oftentimes end user and particularly IT administrators do not have full transparency about the exact nature of documents to be imported. Hence, the result of an import might range between "great", "acceptable" or "disastrous", depending on the conversion results.

We distinguish two major evaluation criteria for import success:
- User validation, which depends on the document user to judge the import result
- Formal validation, tracking conversion issues 

We argue that both criteria are potentially crucial for the acceptance and ultimate success of an organization switching to Docs.

The criteria can also help organizations stop switching to Docs at an early stage, if Docs can not fulfill requirements. Similarly, conversion issue reporting could fuel Docs feature development and roadmapping.

### Data destination

The import of documents will mainly be done using the Docs/BlockNote APIs.

While proper unit testing should prevent most errors, it may still happen that:
- The Docs API is temporarily unavailable
- The Docs API will return errors for invalid input data

For both aspects, proper reporting should be implemented.

## Reporting conversion issues

For tracking formal validation issues encountered during document conversion, we draft an initial reporting format. It is described in [document-conversion-reporting-format.md](https://github.com/docspec-hackathon/documentation/blob/main/document-conversion-reporting-format.md).

## Importing .docx to Docs

As an initial Proof-of-Concept, we implemented the import of ".docx" files into La Suite Docs. Aspects covered by our implementation are highlighted green in the diagram.

![Overview describing aspects in the migration of Documents to Docs (highlighting implemented aspects)](/assets/lasuite-docs-migration-big-picture.drawio-highlighted.png)

The implementation has two parts:
- The actual conversion of ".docx" to a BlockNote data structure
- Making the import feature available for Docs users

### Conversion
- See https://github.com/docspec-hackathon/import-api for code

### User experience
- See https://github.com/docspec-hackathon/docs for fork of La Suite docs using interface improvements:
    - Import button 
    - Show issue report
    
