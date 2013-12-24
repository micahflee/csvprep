# CSV Prep

CSV Prep is a tool for helping you format your CSV for import into [Overview](https://www.overviewproject.org/).

When you import a CSV into Overview it ignores all columns except these: 'text', 'title', 'url', 'id', and 'tags' (case-insensitive). But your dataset might include other columns of data that you want to be able to search through using Overview. An easy way to do this is to append those other columns to the end of 'text', the main body column.

I wrote it quickly and fairly sloppily with a klunky user interface, but it works. You can use it to load a CSV, set the values of the header row (or rename the existing header row), and merge columns together.

## Usage

    Usage: ./csvprep input.csv output.csv [--escape_quotes]
      The input and output CSV filenames are required.
      Add --escape_quotes if the input CSV contains quotes escaped like '\"' instead of '""'

## Example

In this example, CSV Prep is prepping the full set of diplomatic cables that Wikileaks accidentially released in a torrent for import into Overview.

The original file, cables.csv, doesn't contain any column headers. If it did contain headers though, they would be something like: ID, Date, Reference ID, Origin, Classification, Source, Header, Text -- with Text being the main body. Additionally, the original file escapes it's quotes like \", but Overview requires that quotes get escaped by using double quotes, "".

In order to import this into Overview, we need to add headers. But if we want to be able to access all of the data, then we need to take the values of the fields that Overview doesn't know about (such as Classification, or Header) and append them to the end of the Text field.

Here's how to do this with CSV Prep:

    micah@skywalker ~ $ csvprep cables.csv formatted_cables.csv --escape-quotes
    Welcome to CSV Prep, a tool to help you format your CSV for importing into Overview.

    ['1', '12/28/1966 18:48', '66BUENOSAIRES2481', 'Embassy Buenos Aires', 'UNCLASSIFIED', '66STATE106206', 'P R 281848Z DEC 66\nFM AMEMBASSY BUENOS AIRES\nTO SECSTATE WASHDC PRIORITY\nINFO USCINCSO\nCINCLANT\nAMEMBASSY RIO DE JANEIRO\nAMEMBASSY SANTIAGO\nAMEMBASSY MONTEVIDEO\nAMEMBASSY QUITO\nAMEMBASSY LIMA\nAMEMBASSY MEXICO\nAMEMBASSY OTTAWA\nAMEMBASSY LONDON\nSTATE GRNC', 'UNCLASSIFIED BUENOS AIRES 2481 \n \nOriginal Telegram was Confidential but has since been \nde-classified \n \n--------------------------------------------- ---- \nCopy from the National Archives \nRG 59: General Records of the Department of state \n1964-66 Central Foreign Policy File \nFile: POL 33-4 ARG \n--------------------------------------------- ---- \n \nE.O. 12958: DECL: DECLASSIFIED BY NARA 09/02/2009 \nTAGS: EFIS, PBTS, AR \nSUBJECT:  EXTENDED NATIONAL JURISDICTIONS OVER HIGH SEAS \n \nREF: STATE 106206 CIRCULAR; STATE CA-3400 NOV 2, 1966 \n \n \n1.  PRESS REPORTS AND VARIETY EMBASSY SOURCES CONFIRM \nNEW ARGENTINE LEGISLATION UNILATERALLY CHANGING SEAS JURIS- \nDICTION NOW UNDER ADVANCED REVIEW.  REPORTEDLY LAW WOULD \nESTABLISH SIX MILE TERRITORIAL SEA, PLUS ANOTHER SIX MILES \nOF EXCLUSIVE FISHING JURISDICTION, PLUS ANOTHER EXTENDED ZONE \nOF \\PREFERENTIAL JURISDICTION\\" FOR FISHING PURPOSES.  DRAFT- ']
    Was that a list of CSV headers? (y/n): n

    What is the header for this line?
    Column: 1
    Header: ID

    What is the header for this line?
    Column: 12/28/1966 18:48
    Header: Date

    What is the header for this line?
    Column: 66BUENOSAIRES2481
    Header: Reference ID

    What is the header for this line?
    Column: Embassy Buenos Aires
    Header: Origin

    What is the header for this line?
    Column: UNCLASSIFIED
    Header: Classification

    What is the header for this line?
    Column: 66STATE106206
    Header: Source

    What is the header for this line?
    Column: P R 281848Z DEC 66
    FM AMEMBASSY BUENOS AIRES
    TO SECSTATE WASHDC PRIORITY
    INFO USCINCSO
    CINCLANT
    AMEMBASSY RIO DE JANEIRO
    AMEMBASSY SANTIAGO
    AMEMBASSY MONTEVIDEO
    AMEMBASSY QUITO
    AMEMBASSY LIMA
    AMEMBASSY MEXICO
    AMEMBASSY OTTAWA
    AMEMBASSY LONDON
    STATE GRNC
    Header: Header

    What is the header for this line?
    Column: UNCLASSIFIED BUENOS AIRES 2481 
     
    Original Telegram was Confidential but has since been 
    de-classified 
     
    --------------------------------------------- ---- 
    Copy from the National Archives 
    RG 59: General Records of the Department of state 
    1964-66 Central Foreign Policy File 
    File: POL 33-4 ARG 
    --------------------------------------------- ---- 
     
    E.O. 12958: DECL: DECLASSIFIED BY NARA 09/02/2009 
    TAGS: EFIS, PBTS, AR 
    SUBJECT:  EXTENDED NATIONAL JURISDICTIONS OVER HIGH SEAS 
     
    REF: STATE 106206 CIRCULAR; STATE CA-3400 NOV 2, 1966 
     
     
    1.  PRESS REPORTS AND VARIETY EMBASSY SOURCES CONFIRM 
    NEW ARGENTINE LEGISLATION UNILATERALLY CHANGING SEAS JURIS- 
    DICTION NOW UNDER ADVANCED REVIEW.  REPORTEDLY LAW WOULD 
    ESTABLISH SIX MILE TERRITORIAL SEA, PLUS ANOTHER SIX MILES 
    OF EXCLUSIVE FISHING JURISDICTION, PLUS ANOTHER EXTENDED ZONE 
    OF \PREFERENTIAL JURISDICTION\" FOR FISHING PURPOSES.  DRAFT- 
    Header: Text

    Here are the new headers: ['ID', 'Date', 'Reference ID', 'Origin', 'Classification', 'Source', 'Header', 'Text']
    Are these headers good? (y/n): y

    Overview ignores all headers except these: ['text', 'title', 'url', 'id', 'tags']
    Here are your current headers: ['ID', 'Date', 'Reference ID', 'Origin', 'Classification', 'Source', 'Header', 'Text']

    Would you like to rename any of your headers? (y/n): y
      0: ID
      1: Date
      2: Reference ID
      3: Origin
      4: Classification
      5: Source
      6: Header
      7: Text
    Which header would you like to rename? [0, 1, 2, 3, 4, 5, 6, 7] 1

    What should the new header be? Title

    Overview ignores all headers except these: ['text', 'title', 'url', 'id', 'tags']
    Here are your current headers: ['ID', 'Title', 'Reference ID', 'Origin', 'Classification', 'Source', 'Header', 'Text']

    Would you like to rename any of your headers? (y/n): n

    Overview ignores all headers except these: ['text', 'title', 'url', 'id', 'tags']
    Here are your current headers: ['ID', 'Title', 'Reference ID', 'Origin', 'Classification', 'Source', 'Header', 'Text']

      0: Merge a column into another column
      1: Explode a merged column
      2: All done
    Which would you like to do? [0, 1, 2] 0

      0: ID
      1: Title
      2: Reference ID
      3: Origin
      4: Classification
      5: Source
      6: Header
      7: Text
    Which column would you like to merge into? [0, 1, 2, 3, 4, 5, 6, 7] 7

      0: ID
      1: Title
      2: Reference ID
      3: Origin
      4: Classification
      5: Source
      6: Header
      7: Text
    And which column would you like to merge? [0, 1, 2, 3, 4, 5, 6, 7] 6

    Overview ignores all headers except these: ['text', 'title', 'url', 'id', 'tags']
    Here are your current headers: ['ID', 'Title', 'Reference ID', 'Origin', 'Classification', 'Source', 'Text, Header']

      0: Merge a column into another column
      1: Explode a merged column
      2: All done
    Which would you like to do? [0, 1, 2] 0

      0: ID
      1: Title
      2: Reference ID
      3: Origin
      4: Classification
      5: Source
      6: Text, Header
    Which column would you like to merge into? [0, 1, 2, 3, 4, 5, 6] 6

      0: ID
      1: Title
      2: Reference ID
      3: Origin
      4: Classification
      5: Source
      6: Text, Header
    And which column would you like to merge? [0, 1, 2, 3, 4, 5, 6] 5

    Overview ignores all headers except these: ['text', 'title', 'url', 'id', 'tags']
    Here are your current headers: ['ID', 'Title', 'Reference ID', 'Origin', 'Classification', 'Text, Header, Source']

      0: Merge a column into another column
      1: Explode a merged column
      2: All done
    Which would you like to do? [0, 1, 2] 0

      0: ID
      1: Title
      2: Reference ID
      3: Origin
      4: Classification
      5: Text, Header, Source
    Which column would you like to merge into? [0, 1, 2, 3, 4, 5] 5

      0: ID
      1: Title
      2: Reference ID
      3: Origin
      4: Classification
      5: Text, Header, Source
    And which column would you like to merge? [0, 1, 2, 3, 4, 5] 4

    Overview ignores all headers except these: ['text', 'title', 'url', 'id', 'tags']
    Here are your current headers: ['ID', 'Title', 'Reference ID', 'Origin', 'Text, Header, Source, Classification']

      0: Merge a column into another column
      1: Explode a merged column
      2: All done
    Which would you like to do? [0, 1, 2] 0

      0: ID
      1: Title
      2: Reference ID
      3: Origin
      4: Text, Header, Source, Classification
    Which column would you like to merge into? [0, 1, 2, 3, 4] 4

      0: ID
      1: Title
      2: Reference ID
      3: Origin
      4: Text, Header, Source, Classification
    And which column would you like to merge? [0, 1, 2, 3, 4] 3

    Overview ignores all headers except these: ['text', 'title', 'url', 'id', 'tags']
    Here are your current headers: ['ID', 'Title', 'Reference ID', 'Text, Header, Source, Classification, Origin']

      0: Merge a column into another column
      1: Explode a merged column
      2: All done
    Which would you like to do? [0, 1, 2] 0

      0: ID
      1: Title
      2: Reference ID
      3: Text, Header, Source, Classification, Origin
    Which column would you like to merge into? [0, 1, 2, 3] 3

      0: ID
      1: Title
      2: Reference ID
      3: Text, Header, Source, Classification, Origin
    And which column would you like to merge? [0, 1, 2, 3] 2

    Overview ignores all headers except these: ['text', 'title', 'url', 'id', 'tags']
    Here are your current headers: ['ID', 'Title', 'Text, Header, Source, Classification, Origin, Reference ID']

      0: Merge a column into another column
      1: Explode a merged column
      2: All done
    Which would you like to do? [0, 1, 2] 2


    Input csv already have headers? False
    Here are the headers: ['ID', 'Title', 'Reference ID', 'Origin', 'Classification', 'Source', 'Header', 'Text']
    Here is the merge data: [[0], [1], [7, 6, 5, 4, 3, 2]]

    Writing row #251286

    CSV file written: formatted_cables.csv

The new CSV, formatted_cables.csv, is ready to import into Overview. It only has three columns now, ID, Title, and Text, but the Text column also contains the data from Header, Source, Classification, Origin, and Reference ID.
