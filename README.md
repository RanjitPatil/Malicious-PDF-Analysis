# Malicious PDF Analysis

## Understand the PDF file structure

**1. Header -** Contains the version number of the pdf file.

**2. Body -** Contains objects - obj values (number) denotes its name and its version number, obj & endobj refers to the beginning and end of an object.

**3. Cross Reference Table -** Specifies the offset from the start of the file to each object in the file, so that the PDF reader will be able to locate them without loading the whole document, begins with the keyword xref.

**4. Trailer -** Contains overall info about the PDF, points to the start of Cross Reference Table.



![image](https://user-images.githubusercontent.com/43460691/208238136-81d3926f-1a81-45ab-bf9a-fe207c73c6b5.png)
![image](https://user-images.githubusercontent.com/43460691/208238820-669ea948-8466-41a4-a9ce-8c076ee15c66.png)


## PDF file Actions :

**1. /OpenAction /AA -** The function of this element is to carry out an action for e.g. execute a script.

**2. /JavaScript /JS -** Link to the JavaScript that will run when the PDF is opened.

**3. /Names -** Names of files that will likely be referred to by the PDF itself.

**4. /EmbeddedFile -** Shows the other files embedded within the PDF file itself e.g., scripts.

**5. /URI /SubmitForm -** Links to other URLs on the internet e.g., possible link to a 2nd stage payload/additional tools for malware to run.

**6. /Launch -** Similar to OpenAction, can be used to run embedded scripts within the PDF file itself or run new additional files that have been downloaded by the PDF.


## Actions of elements that describe how a PDF works :

- **/OpenAction /AA -** This element's function is to carry out an action, such as running a script.

- **/JavaScript /JS -** Link to the JavaScript that will run when the PDF is opened.

- **/Names -** File names that will most likely be referred to by the PDF itself.

- **/EmbeddedFile -** Shows other files embedded within the PDF file, such as scripts.

- **/URI /SubmitForm -** Links to other URLs on the internet.

- **/Launch -** Used to run embedded scripts within the PDF file itself or run new additional files that have been downloaded by the PDF.

## String and Data Encoding

PDF can encode strings in multiple ways to obfuscate data,Below are the encoding examples :

![image](https://user-images.githubusercontent.com/43460691/208233540-9b6b7a92-3b19-4df8-97ef-d602a4304682.png)


PDF also uses **Filters** to decode the encoded data, which tell the PDF reader that the corresponding string is supposed to be decoded using the provided method.

![image](https://user-images.githubusercontent.com/43460691/208233728-3895976e-4075-42ab-a93a-1362992daaf5.png)

## Tools used for Analysis

> **pdfid -** Identifies PDF object types and filters.

> **pdf-parser -** Parses, Searches and Extracts data from PDF documents.

> **peepdf -** Combination of pdfid & pdf-parser, as it is able to find suspicious objects, decode data and has JavaScript analysis built-ins

## Malware Sample

> **MD5:** 2264DD0EE26D8E3FBDF715DD0D807569

> **SHA256:** ad6cedb0d1244c1d740bf5f681850a275c4592281cdebb491ce533edd9d6a77d

![image](https://user-images.githubusercontent.com/43460691/208060601-33e1377c-7130-4597-9ec7-ae7a6aaa1dc3.png)

## Tool - pdfid

> ***`REMnux: pdfid.py "location of badpdf.pdf file"`***

- The output indicates PDF version is 1.3 and PDF contain 14 Objects, 2 Streams and JavaScript objects.


![image](https://user-images.githubusercontent.com/43460691/208269358-102f0d01-9926-4090-b187-062beb83c5d2.png)
 

## Tool - pdf-parser

- pdf-parser will extract all data from the PDF. In order to narrow down our search we need to use the built-in command options such as ‘–Search’.

- Use pdfparser with –search to show the /OpenAction object

> ***`REMnux: pdf-parser.py --search openaction badpdf.pdf`***


![image](https://user-images.githubusercontent.com/43460691/208269784-d3322e4d-c360-4da2-b389-7af14f06f0ec.png)

- Now let’s search for the Javascript object with pdfparser

> ***`REMnux: pdf-parser.py --search javascript badpdf.pdf`***

![image](https://user-images.githubusercontent.com/43460691/208270822-a637ac47-81d0-4914-bce4-b0a038359c29.png)

- Now let’s search for the Javascript object 10 and 13.

> ***`REMnux: pdf-parser.py --object 10 badpdf.pdf`***

> ***`REMnux: pdf-parser.py --object 13 badpdf.pdf`***

- Object 10 references boject 12 and its calling the /Namnes object (New_Script)

- Object 13 stores the actual Javascript. It contain /Filter and /FlatDecode action elements, That means it is compressed.


![image](https://user-images.githubusercontent.com/43460691/208271229-15edb796-1ceb-44d5-82ab-2deaee61539a.png)


- Now let’s search for the Javascript object 13, We will use the -f (filter) & -w (raw output) to check this object.

> ***`REMnux: pdf-parser.py --object 13 -f -w badpdf.pdf`***

![image](https://user-images.githubusercontent.com/43460691/208271756-7d526e0b-9392-4904-997a-3fbd9343eaba.png)

- To check JavaScript code we need to dump the code into seprate find and will use JavaScript editior or pee-pdf tool.

> ***`REMnux: pdf-parser.py --object 13 -f -w -d obj13 badpdf.pdf`***

![image](https://user-images.githubusercontent.com/43460691/208271865-c0fa5527-b257-43f3-b823-d9f74eaec199.png)

- We will use pee-pdf tool to look JavaScript.

## Tool - peepdf

![image](https://user-images.githubusercontent.com/43460691/208271979-736af618-994b-424e-8f5c-99c86acb0e32.png)

- Use below command to downlode js file in peepdf.

> ***`REMnux: PPDF> object 13 > obj13.js`***

![image](https://user-images.githubusercontent.com/43460691/208673609-0dfe52cf-a1fc-465b-9dea-27757ed7d58a.png)

## Script Obfucsation Techniques :

- **Formatting -** Modifies the format of the code to make it defficult to read.

- **Extraneous Code -** Add extra lines of code to confuse analysts.

- **Data Obfucsation -** Use operations to make data unreadable of confusing.

- **Substitution -** Modify the veriable names to random and meaningless names.

![image](https://user-images.githubusercontent.com/43460691/208677682-a5f8d908-d44d-4630-9680-a0b3b96c192e.png)



















