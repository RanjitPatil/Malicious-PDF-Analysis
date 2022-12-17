# PDF Analysis

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

![image](https://user-images.githubusercontent.com/43460691/208060601-33e1377c-7130-4597-9ec7-ae7a6aaa1dc3.png)

## Tools used for Analysis

> **pdfid -** identifies PDF object types and filters.

> **pdf-parser -** parses, searches and extracts data from PDF documents.

> **peepdf -** is the combination of pdfid & pdf-parser, as it is able to find suspicious objects, decode data and has JavaScript analysis built-ins

## Actions of elements that describe how a PDF works

- **/OpenAction /AA -** the function of this element is to carry out an action for e.g. execute a script

- **/JavaScript /JS -** link to the JavaScript that will run when the PDF is opened

- **/Names -** names of files that will likely be referred to by the PDF itself

- **/EmbeddedFile -** shows the other files embedded within the PDF file itself e.g., scripts

- **/URI /SubmitForm -** Links to other URLs on the internet e.g., possible link to a 2nd stage payload/additional tools for malware to run

- **/Launch -** Similar to OpenAction, can be used to run embedded scripts within the PDF file itself or run new additional files that have been downloaded by the PDF

## String and Data Encoding

PDF can encode strings in multiple ways to obfuscate data,Below are the encoding examples :

![image](https://user-images.githubusercontent.com/43460691/208233540-9b6b7a92-3b19-4df8-97ef-d602a4304682.png)


PDF also uses **Filters** to decode the encoded data, which tell the PDF reader that the corresponding string is supposed to be decoded using the provided method.

![image](https://user-images.githubusercontent.com/43460691/208233728-3895976e-4075-42ab-a93a-1362992daaf5.png)




