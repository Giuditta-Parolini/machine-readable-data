# Machine-Readable Data Formats in Biodiversity Informatics
## Recommendations and Best Practices
##### *Project idea: Giuditta Parolini, Data Scientist, Museum für Naturkunde Berlin, Germany*

------
------

### Table of Contents
- [Preamble](#preamble)
- [Introduction](#introduction)
- [What does machine-readable mean?](#definition)
- [Why do machine-readable data matter for biodiversity science?](#biodiversity)
- [References](#references)
- [Further readings](#further)
- [Acknowledgements](#acknowledgements)
------
------
<br/>

### <a id="preamble">Preamble</a> 
This Guide is written in [Markdown](https://www.markdownguide.org) as an invitation to start exploring tools with higher potential for machine-readability and information sharing compared to standard word processors. Markdown is a lightweight markup language that can be used for a variety of different tasks, from creating a website to writing a book. A document in Markdown format can be opened and edited using any text editor and does not require dedicated software like a PDF or a DOCX file. The trade-off is that styling options are limited compared to standard word processors, but human-readability remains satisfactory.

If you wish to see the rendered Markdown document, there are many online and offline open-source editors available (e.g., [VSCode](https://code.visualstudio.com) + Markdown extensions). These editors are all largely compatible, but Markdown has many flavors and different editors may render some elements of this document in a slightly different fashion. A few Markdown editors do not support HTML style elements. This will prevent you from accessing the internal links in the *Table of Contents* and in the *References* in this document. If possible, choose a Markdown editor that also supports HTML.

If you prefer to consult this guide in a more human-readable format, this is not an issue. A Markdown document can be turned into a PDF in a few clicks. This document can even be published to a webpage, as the transformation in HTML is equally straightforward. You can then decide to read this document as a human reader would, have a computer extract automatically pieces of information that are of special interest to you, even scrape the data when this document is publicly accessible on a webpage.

Markdown integrates seamlessly with version control systems and can, therefore, be used for collaborative projects. This Guide is published as a GitHub repository to give multiple authors the opportunity to contribute. If you wish to improve this document or you have comments and suggestions after reading it, you are welcome to create an issue in GitHub or make a Pull request. 
<br/>

### <a id="introduction">Introduction</a> 
This overview of recommendations and best practices for creating and sharing machine-readable data in biodiversity informatics wishes to contribute to the development of [FAIR](https://www.go-fair.org/fair-principles/) and sustainable data practices. The availability of machine-readable data is a key usability requirement, as it enables data sharing, (re)use, and integration at scale, and provides opportunities for automated quality control.

**Paradoxical as it may sound, however, some of the most popular file formats, e.g., PDF, are not suitable for creating and transferring machine-readable data.** For instance, tabular data embedded in a PDF file such as a journal article, are human-readable, but cannot be accessed directly by a computer, while the same data presented in a properly formatted CSV file are machine-readable.
Another interesting example is the DOCX format, which is very popular among word processors. The DOCX format is based on the standard Office Open XML which was defined to foster "interoperability across office productivity applications and line-of-business systems, as well as to support and strengthen document archival and preservation, all in a way that is fully compatible with the existing corpus of Microsoft Office documents" [(ISO/IEC, 2016)](#iso). In principle, a DOCX file can be easily parsed being based on the XML standard, in practice the same example described above, i.e., the extraction of a data table from an article manuscript in DOCX format, requires labour, starting with accessing the multiple files which are hidden within the DOCX format, recovering then the table-only content in the file, and eventually exporting the table data in a machine-readable format like CSV for further use.

When we take into account biodiversity science drive towards data sharing and openness, an additional consideration worth making is that large part of automated information sharing takes place via the Internet nowadays. Data can be transferred and distributed via web APIs using XML and JSON format, but data can also be scraped directly from webpages, if permitted by intellectual property laws and regulations. Also in this case, however, the data table in the example mentioned above is not likely to be easily machine-readable. Files in PDF and DOCX format can be transformed in HTML for web publication, but the results are usually poor when complex styling options are used in the original file, as it is often the case with word processors. A web scraping effort would therefore be laborious and error-prone.

**Before choosing a data format due consideration should always be given, among other things, to its machine-readability.** Only very small datasets with at most a few hundred entries can be processed directly by humans. For all the other datasets, only machine processing is a viable solution, but computers can work with data only when the requirement of machine-readability is satisfied. Providing a dataset in a non machine-readable format forces the user to laborious preprocessing and makes the chance to introduce mistakes in the original data a real issue. Non machine-readable datasets run the risk to be forgotten and ignored regardless of their scientific value. The aim of this guide is to clarify the importance of producing machine-readable data and help data managers and biodiversity researchers select the best machine-readable format according to their needs.

The document begins presenting the concept of machine-readable data and why it is especially valuable in biodiversity informatics. Its core part is filled with suggestions and recommendations for machine-readable data formats suitable for biodiversity informatics. In this section, both machine-readable data formats of general use, like CSV, and machine-readable data formats that are specific to science, like NetCFD (Network Common Data Form), are discussed. A final section will sketch a few considerations about the value (and pitfalls) of machine-readable data in the age of AI.
<br/>

### <a id="definition">What does machine-readable mean?</a>  
The concept of machine-readable data has a long history. It was introduced in the 1960s to refer to the physical input formats, such as magnetic tape and punched cards, typical for computers at the time, and was at the bottom of the development of the MARC (Machine-Readable Cataloging) programme initiated by the Library of Congress in the US to automate library operations [(Avram, 2003)](#avram). Nowadays, the concept of machine-readability has shifted from the realm of the physical media used to feed data into a computer to the choice of a suitable digital format for automatic data processing.

The Open, Public, Electronic, and Necessary Government Data Act (2017-2018), which was passed by the US Congress, defines a machine-readable data format as "a format in which information or data can be easily processed by a computer without human intervention while ensuring no semantic meaning is lost" [(OPEN Government Data Act §3561(7))](#usdataact). The European Union takes its definition of [machine-readability](https://eur-lex.europa.eu/eli-register/glossary.html) from the Open Data Handbook. [Here](http://opendatahandbook.org/glossary/en/terms/machine-readable/), a machine-readable data format is defined as a structured data format that can be automatically read and processed by a computer. The definitions cited can be considered equivalent as the existence of a structured data format is a pre-requisite for maintaining the semantic meaning while automatically processing the data. A CSV document is an example of structured data because, for each data point (each row of the CSV file), a certain amount of information, i.e., the column values, is provided.

It is important to point out that the file extension, e.g. .csv, is a necessary, but not a sufficient condition to have machine-readable data. It is necessary, because the data format must be structured. Not only CSV, but also XML, JSON, etc. fulfil the requirement of being structured data formats and the choice of one over the other depends on the type of data examined and the specific use case. The file extension, however, is not sufficient, because a badly formatted spreadsheet with headers on multiple rows, deviations from the tabular format, improper use of the column delimiters in the column values, etc. cannot be turned into a machine-readable file just by saving the spreadsheet in CSV format. The CSV will be invalid and any attempt to read it, regardless of the software tool used, will result in an error message. It should be evident in a similar fashion that **electronic access to a document does not mean that the document is machine-readable**. For instance, coming back to the example cited in the introduction, a PDF version of an originally printed journal article is not likely to be machine-readable. This becomes quickly evident by looking at the website of a scientific publisher with a notable tradition such as the [Royal Society](https://royalsocietypublishing.org/journal/rstb). PDF copies of scanned images of the print-only articles are displayed online, but with a warning for readers. The only piece of text available on the webpage is the abstract and the web crawlers are authorised to access it, but readers are warned that the abstract can contain typos, as it has been automatically harvested from scanned images of the printed version using Optical Character Recognition (OCR). Aside from the abstract, the Royal Society has made no attempt to make the data contained in its older articles, for instance, a table, machine-readable, likely due to the considerable investment of time and resources that this would required. Indeed, once data have been produced in a non machine-readable format, their transformation into a machine-readable format is always an expensive (time, money, and human resources) and complex task that leaves plenty of room for errors and can considerably lower data quality.

In summary, **machine-readable data only** need to satisfy the criteria mentioned above, i.e., they **need to be digital (but being electronically available is not enough) and to use a valid structured data format that conserves the semantic meaning**. These requirements have some interesting consequences that merit more attention than they usually receive.

a) **Machine-readability is not defined in contrast or opposition to human-readability.** Unsurprisingly, therefore, machine-readable data are in many cases also human-readable. Data in CSV, XML, or JSON format, for instance, can be inspected visually and many code editors can greatly enhance human-readability for these machine-readable formats using indentation and different colours according to the components of the data structure. The fact that machine-readable data formats can be rendered on the screen in an appealing style, though, should not be confused and equated with the opportunity to style tables and documents offered by word processors and electronic spreadsheet software generating DOCX and XLSX files. While in the former example, the styling is superimposed at the display stage to make the information more appealing to the human eye, in the second case, instead, the style elements (for instance text boxes in a spreadsheet) are intrinsic to the construction of the file and they constitute an hindrance to machine-readability. 

b) **Images are typically not machine-readable.** With the notable exception of barcodes and watermarks **[1]**, images are not machine-readable because the information they provide does not follow a specific data structure. This is true for holiday photos as well as for scientific images produced by microscopes, CT scans, infrared cameras, and other equipment commonly used in scientific research. Images produced with digital equipment, though, usually can (and should) have associated metadata in machine-readable format. In addition, although the semantic meaning of images cannot be directly accessed by machines, computer vision algorithms for image segmentation and object detection have been in use for quite some time to facilitate information extraction from images and their automatic labelling.

**[1]** Barcodes and watermarks are image-based data interfaces. The information they encode can be recovered from their representation, for instance in print, via a sensor such as the camera of a mobile phone. Popular barcodes are the universal product code (UPC), the quick response (QR) code, the Aztek code, and the Data Matrix [(Sharma, 2016)](#sharma). While barcodes work by embedding the data in the image pattern, watermarks hide the embedded data in an image  

c) **There are potentially no limitations to the complexity of the data structures in machine-readable formats like CSV, XML, or JSON, nor these data formats have limitations to the number of data points they can support.** On the contrary, Excel XLSX files (but the same is true for other proprietary spreadsheet software) have limitations in both the number of columns and rows that they support. The limit was set by the developers of this proprietary software to avoid overloading memory and computing capabilities of the average computer user. There are no such limitations for machine-readable data formats like CSV, XML, or JSON, but, of course, parsing and editing larger and larger data files takes longer and longer until computational and memory capacity of the hardware used are reached.
 
<br/>

### <a id="biodiversity">Why do machine-readable data matter for biodiversity science?</a>  
At the time of writing (June 2024) the Global Biodiversity Information Facility [GBIF](https://www.gbif.org) makes available via its partner institutions over 100.000 datasets amounting to several millions data records on plants, animals, and natural environments. These data range from taxonomic checklists to species observations to images and other media of digitised natural history collections. 

While the raw data in themselves might not be machine-readable, for instance, this is the case for the digital images of collection specimens, all metadata for the records and all the tabular data are made available in a machine-readable format, such as tab delimited CSV files or XML files, following one of the data standards popular in biodiversity science. This makes all the records searchable and retrievable not just manually, but also automatically using the [GBIF API](https://techdocs.gbif.org/en/openapi/). 

Given the amount of records under examination, it becomes quickly apparent that having available information in a machine-readable format offers the opportunity to access data at scale, combine them for analysis that goes beyond the original aims of their creators, and redistribute them to a larger public. Yet, this is not always the case, especially with the smaller datasets associated to scientific articles. Due to the lack of a general policy for biodiversity science publications and the fact that biodiversity research appears in journals belonging to different disciplines, it is not uncommon to still find published biodiversity data only available in tables saved in DOCX files or compiled in spreadsheets that are not machine-readable. An even greater concern is for the unpublished data produced during research projects. The increased availability and usage of data management tools and platforms facilitates the implementation of best practices, but it is not ***per se*** a guarantee that the data created are machine-readable. For this reason, this guide provides an overview of suitable machine-readable data formats for biodiversity research, illustrates their context of application, and gives advice against possible pitfalls in their implementation.


<br/>

### General formats for machine-readable data
* #### Tabular data
* #### Geographic data
* #### Images
* #### Other media
<br/>

### Formats for machine-readable data specific to biodiversity science
<br/><br/>

### Machine-readable data in the age of AI: Some final remarks
<br/><br/>

### <a id="references">References</a>
<a id="avram">Avram</a>, E.D. (2003) Machine-Readable Cataloging (MARC) Program. In *Encyclopedia of Library and Information Science* 3, pp.1712-1730. DOI: [10.1081/E-ELIS 120008993](https://www.taylorfrancis.com/chapters/edit/10.1081/E-ELIS3-120008993/machine-readable-cataloging-marc-1961–1974-elis-classic-henriette-avram).
<br/>

<a id="iso">ISO/IEC</a> STANDARD 29500-1: 2016(E) (2016) Information technology - Document description and processing languages: Office Open XML File Formats. Vernier, Geneva, Switzerland: ISO Copyright Office [(available online)](https://standards.iso.org/ittf/PubliclyAvailableStandards/c071691_ISO_IEC_29500-1_2016.zip).
<br/>

<a id="sharma">Sharma</a>, G. (2016) Image-based data interfaces revisited: Barcodes and watermarks for the mobile and digital worlds, *8th International Conference on Communication Systems and Networks (COMSNETS)*, Bangalore, India, pp. 1-6. DOI: [10.1109/COMSNETS.2016.74400213](https://ieeexplore.ieee.org/document/7440021).
<br/>

<a id="usdataact">OPEN Government Data Act</a> H.R.1770 115th Congress (2017-2018) [(available online)](https://www.congress.gov/115/bills/hr1770/BILLS-115hr1770ih.pdf).
<br/>

<br/><br/>

### <a id="further">Further readings</a> 
<br/><br/>

### <a id="acknowledgements">Acknowledgements</a>  
This research was supported by the German Research Foundation (DFG) under grant number 528674292. 
<br/>

------
------

