MIDV-500: A Dataset for Identity Documents Analysis and Recognition on Mobile Devices in Video Stream

--------------------------------------------------------------------------------

Contents:

1. Overview
2. Structure
3. Ground truth
4. Miscellaneous
5. Contact information
6. Journal reference

--------------------------------------------------------------------------------

1. Overview

A lot of research has been devoted to identity documents analysis and recognition on 
mobile devices. Mobile Identity Document Video dataset (MIDV-500) consists of 500 video 
clips for 50 different identity document types with ground truth which allows to perform 
research in a wide scope of various document analysis problems.

Since an important feature of identity documents is their sensitiveness as they contain 
personal data, all source document images used in MIDV-500 are either in public domain 
or distributed under public copyright licenses.

--------------------------------------------------------------------------------

2. Structure

A list of 50 document types used in this dataset is presented in sources table /sources-index.pdf. 
This table contains document type number, code which is used in MIDV-500, description, link
to original image in Wikimedia Commons, attribution note and list of modifications performed
to the original image before using it for this dataset. For document types listed in PRADO database
a link to appropriate PRADO page is also presented in this table.

In /dataset directory data for each document type is placed in a separate archive. You can check MD5
hashsum for each archite using references in /md5.txt.

Structure of each archive:

XX_DOC_TYPE_CODE.zip:
  /videos
    - TAXX.MOV
    - TSXX.mp4
    - ...
  /images
    - XX_DOC_TYPE_CODE.tif
    - TA/
      - TAXX_01.tif
      - TAXX_02.tif
      - ...
    - ...
  /ground_truth
    - XX_DOC_TYPE_CODE.json
    - TA/
      - TAXX_01.json
      - TAXX_02.json
      - ...

Directory /videos contain 10 original videos of the document shot on two devices. First letter of 
video name indicates the condition (_T_able, _K_eyboard, _H_and, _P_artial, _C_lutter), the second
letter - device ('A' for Apple iPhone 5 and 'S' for Samsung Galaxy S3 (GT-I9300)). In order to shoot
the videos each modified document image was printed on photo paper using laser color printer and
laminated using glossy laminating film.

Directory /images, first of all, contains modified image which has been used to shoot the set of
corresponding videos /images/XX_DOC_TYPE_CODE.tif. Then it contains 10 directories for each video, 
and each directory contain 30 frames of this video onto which the first 3 seconds of each video has
been split. Splitting was performed using ffmpeg v4.0 built with gcc 8.1.0 using parameters "-r 10 -q:v 1".

Directory /ground_truth is isomorphic to /images directory and contains ground truth for each image.

--------------------------------------------------------------------------------

3. Ground truth

Ground truth format for modified image /images/XX_DOC_TYPE_CODE.tif (/ground_truth/XX_DOC_TYPE_CODE.json):

{
  "field01": {
    "value": "Erika",
    "quad": [ [983, 450],  [1328, 450],
              [1328, 533], [983, 533] ]
  },
  // ...
  "photo": {
    "quad": [ [78, 512],   [833, 512],
              [833, 1448], [78, 1448] ]
  }
}

Thus for each text field a UTF-8 ideal value is provided and a bounding quadrangle. Points in quadrangles
are sorted in order: top-left, top-right, bottom-right, bottom-left, coordinates are given as a pairt [x, y] 
denoted in pixels. Note that the first point of the quadrangle correspond to the top-left corner of the
rectified field (example - "field07" in document 39). At most two fields has special names and don't have 
UTF-8 value: "photo" and "signature".

Note that for two documents UTF-8 values are either fully omitted ("*" value is used instead) or partially
omitted ("*" is a substring of the value). This is true for document 29 (ideal values are in Farsi) and for
document 18 (ideal values are in Arabic).

Ground truth format for each frame:

{
  "quad": [ [0, 0],     [111, 0],
            [111, 222], [0, 222] ]
}

Thus for each frame a document boundaries quadrangle is provided. Points in quadrangles are sorted in 
order: top-left, top-right, bottom-right, bottom-left, coordinates are given as a pairt [x, y] denoted 
in pixels. If the corner of the document is not visible on the frame, coordinates will point outside
the frame (so, if the document is not visible on the frame at all, all four points will lay outside
the frame).

--------------------------------------------------------------------------------

4. Miscellaneous

To users of the dataset who now Arabic and/or Farsi: authors will greatly appreciate if somebody provides
ideal UTF-8 representations of text fields in documents 29 and 18. 

Authors are deeply grateful to Manabu Iwasaki for providing ground truth for Chinese and Japanese fields.

--------------------------------------------------------------------------------

5. Contact information

Any questions, complaints, feature requests, etc. can be directed to: 
kbulatov@smartengines.ru (Konstantin Bulatov)

6. Journal reference

An article about this dataset is published in Computer Optics 43(5) 2019.
http://www.computeroptics.smr.ru/eng/KO/Annot/KO43-5/430515e.html

  Citation: Arlazarov VV, Bulatov K, Chernov T, Arlazarov VL. MIDV-500: a dataset 
            for identity document analysis and recognition on mobile devices in 
            video stream. Computer Optics 2019, 43(5): 818-824. 
            DOI: 10.18287/2412-6179-2019-43-5-818-824.
