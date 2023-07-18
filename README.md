# OCR-based Medical Data Extraction
## Problem statement

There are a lot of procedures that need to be followed by the health insurance companies as per the government regulation to issue the claims, for that the insurance company has to process the images of patient details and prescriptions sent by hospitals or induvial doctors and extract useful data from them. For these processes, most insurance companies outsource workforce from companies like “Mr. X data Analytics” to extract the information from images manually. 

Mr. X data Analytics uses software, which will show the scanned images of patient details or prescriptions, the person needs to type the information by seeing the image manually in the right side column and selecting the type of information. As it is a manual process, errors will be common and dealing with the huge set of images like in the pandemic time, will not be possible with the same amount of workforce. As well the Insurance companies have requested to send the data within 24hrs when it is sent for extraction. All of these constraints forced, Mr. X Data Analytics to consider a software upgrade from their old software. 

## Solution approach

To solve all these problems, we are building a program which can do the extraction of data from images automatically. As always, machines can not replace humans. A person will recheck the extracted data and submit it. So, it will save a tremendous amount which was taken to type the data manually. 

Here, we are using the Python programming language and pytesseract google library for extracting the data and Regex module to process the data and get distilled desired output.


## Technologies used

- Python
- oops
- Pdf2image module
- Opencv
- pytesseract
- Regular expression
- pytest
- Postman
- FastApi

## Workflow

![workflow](https://github.com/UjasPR/Healthcare-Data-Extraction/assets/138766573/f080da62-fc2f-4ad7-9e59-388b1eb28c52)

### PDF to Image

For converting PDF to image, we have used pdf2image library.

### Without preprocessing extracting data

I tried extracting data from source files without any processing, as they are not in a proper format to be extracted, and the extracted data was not as expected.

![dark_image](https://github.com/UjasPR/Healthcare-Data-Extraction/assets/138766573/7a7c0011-1e07-4840-ace9-cbeed6523be6)

### Extracted data from the above image
```commandline
Dr John Smith, M.D
2 Non-Important Street,
New York, Phone (000)-111-2222

Name: Maria Sharapova Date: 5/11/2022

Address: 9 tennis court, new Russia, DC

—momennannenncmneneunnmnnnnninsissiyoinnitnahaadaanih issn earnttneenrenen:

Prednisone 20 mg
Lialda 2.4 gram

3 days,

or 1 month
```
---
### Image processing

we decided to preprocess the image using OpenCV module, before extracting data from them. For that, we first used normal thresholding and checked, which resulted in below image

![filter_dark](https://github.com/UjasPR/Healthcare-Data-Extraction/assets/138766573/160b2492-1194-40b1-9746-7fd0a0387946)


So, if there is any shadow or some noise, the normal thresholding fades out of the area. which will result in loss of data. 

In the search for a better approach to this problem, we have decided to use the adaptive thresholding technique. In this technique, the image will be divided into sub-image and the thresholding value will be different for all sub-regions.
And the end result of adaptive thresholding is much better compared to normal thresholding.

![adaptive_filter_dark](https://github.com/UjasPR/Healthcare-Data-Extraction/assets/138766573/10f3afb6-e972-484a-9f34-5632cd01b595)


### After preprocessing the image data extraction

```commandline
Dr John Smith, M.D
2 Non-Important Street,
New York, Phone (000)-111-2222

Name: Marta Sharapova Date: 5/11/2022

Address: 9 tennis court, new Russia, DC

K

Prednisone 20 mg
Lialda 2.4 gram

Directions:

Prednisone, Taper 5 mg every 3 days,
Finish in 2.5 weeks a
Lialda - take 2 pill everyday for 1 month
```
---
### Notebook

For all these above trials, I used Jupyter books and developed the small bits of the functionalities., which can be used later while designing the class.

[Notebooks](https://github.com/UjasPR/Healthcare-Data-Extraction/tree/main/Backend/Notebooks)

---
### OOPS design

The code was written using OOPs concepts for extracting the medical data from prescription and patient details documents.

[Code](https://github.com/UjasPR/Healthcare-Data-Extraction/tree/main/Backend/src)

---
### Regular expression

using regular expression module we can match the patterns and extract the data we want from the files. For this project, 
analyst the medical files and in fact all the medical documents will follow the same pattern, we wrote patterns that match only the required data.
Before writing the Python code, It is advisable to practise and match the patterns in regex 101 website.

[regex101](https://regex101.com/)

---
### Test-driven Development

In this project test driven development methodology was used to develop the code. For testing pytest module was used. 
For all the methods and final results, the test cases were designed and checked simultaneously while developing the code.

[Test cases](https://github.com/UjasPR/Healthcare-Data-Extraction/tree/main/Backend/Test)

---
### FastApi

Used FastAPI for hosting the server of the project. FastApi, as name suggest is help us to develop fast and some other advantages are,

- In build Data validation
- In build Documentation
- Fast running and performance

---
### Postman

As it is a backend project, not a developed frontend part. For checking how the server responds to HTTP requests, used Postman to trigger HTTP requests and tested the outcome.

<img width="960" alt="postman" src="https://github.com/UjasPR/Healthcare-Data-Extraction/assets/138766573/d44ccd14-d720-4fdf-83be-1703cc4d91a3">


---
## Result

This backend functionality can be integrated into the Mr.X Analytics existing software and data can be extracted automatically. 
The extracted data may have some errors, the person who is performing the work has to correct it and submit the response.

### Benefits

- Mr. X Analytics can save at least 30 secs for each document. It is small amount of time when looking for one document, but cumulatively it can save a tremendous amount of time which can help the company to complete more documents within the given time and make more profit
- The company doesn't have to hire extra people in the season time.
- As it is a combination of automation and manual the error will be very much low.
