# PDF Analysis using REMnux

## Understand the PDF file structure

**1. Header -** contains the version number of the pdf file.

**2. Body -** contains objects - obj values (number) denotes its name and its version number, obj & endobj refers to the beginning and end of an object.

**3. Cross Reference Table -** Specifies the offset from the start of the file to each object in the file, so that the PDF reader will be able to locate them without loading the whole document, begins with the keyword xref.

**4. Trailer -** contains overall info about the PDF, points to the start of Cross Reference Table.

![This is an image](https://prtksec.github.io/assets/img/pdf_notes/pdf_structure.png)


## PDF file actions

**1. /OpenAction /AA -** the function of this element is to carry out an action for e.g. execute a script.

**2. /JavaScript /JS -** link to the JavaScript that will run when the PDF is opened.

**3. /Names -** names of files that will likely be referred to by the PDF itself.

**4. /EmbeddedFile -** shows the other files embedded within the PDF file itself e.g., scripts.

**5. /URI /SubmitForm -** Links to other URLs on the internet e.g., possible link to a 2nd stage payload/additional tools for malware to run.

**6. /Launch -** Similar to OpenAction, can be used to run embedded scripts within the PDF file itself or run new additional files that have been downloaded by the PDF.

## Malware Sample

> **MD5:** 2264DD0EE26D8E3FBDF715DD0D807569

> **SHA256:** ad6cedb0d1244c1d740bf5f681850a275c4592281cdebb491ce533edd9d6a77d

## Tools used for Analysis

> **pdfid -** identifies PDF object types and filters.

> **pdf-parser -** parses, searches and extracts data from PDF documents.

> **peepdf -** is the combination of pdfid & pdf-parser, as it is able to find suspicious objects, decode data and has JavaScript analysis built-ins

