Pipelines For Data Analysis In R, part 2
========================================================
author: ���N�� Yi-Ju Tseng
autosize: true
font-family: 'Microsoft JhengHei'
navigation: slide

��Ƥ��R�B�J
========================================================
- **��ƶפJ** 
- **��ƲM�~�B�z**���ഫ��Tidy data
- ��Ƥ��R
- ��Ƨe�{�P��ı��

��ƶפJ
====================================
- �q�ɮ׶פJ
- �q�����פJ
- �qTwitter�פJ
- ��ƶץX

�q�ɮ׶פJ
====================================
type:section
- Import Dataset�\�� (RStudio)
- R���� .rds
- R�{�� .R
- �¤�r��� (�L���j)
- ��L�榡

Import Dataset�\�� (RStudio)
====================================
���RStudio�|���ε����k�W����Environment���ҡA���**Import Dataset**

![plot of chunk unnamed-chunk-1](figures/import.png)

Import Dataset�\�� (RStudio)
====================================
- ���`From CSV`
- �I��`Browse`���s�}���ɮ׿����

![plot of chunk unnamed-chunk-2](figures/csv.png)

Import Dataset�\�� (RStudio)
====================================
- �Q�ΤU��`Import Options`���ﶵ�L�հѼ�
    - `Delimiter`���j�Ÿ�
    - `First Row as Names`���C�O�_�����W��
    
![plot of chunk unnamed-chunk-3](figures/csv2.png)

Import Dataset�\�� (RStudio)
====================================
type:alert
incremental:true

- �ާ@[�d���ɮ�](https://raw.githubusercontent.com/CGUIM-BigDataAnalysis/BigDataCGUIM/master/EMBA_BigData/f_lvr_land_a.csv)
- �Y�פJ���ɮ׬�**tab���j��r��**? �Ӧp��վ�ѼơH


R���� .rds
====================================
type:sub-section
�p�G�bR�{�����B�z����ƫ�A�����x�s�@���H�ѫ�����R�A�ϥ�R�����x�s�O�̨Ϊ��覡

- �ɮפp
- Ū���ֳt
- ���˨ϥ�`readRDS()`���Ū��RDS�ɮ�
- [A better way of saving and loading objects in R](http://www.fromthebottomoftheheap.net/2012/04/01/saving-and-loading-r-objects/)

```r
dataset <- readRDS("�ɮ׸��|�P�W��")
```

R�{�� .R
====================================
type:sub-section
- `source`���
- ŪR��Obejct or script, **����**
- **��ھާ@�d��**
    - ���@��example.R�ɦb�u�@���Ҥ�
    - �@�������ɮפ��Ҧ�R���O

```r
source("example.R") 
```

�¤�r��� (�L���j)
====================================
type:sub-section
`readLines`, �v��Ū����r���

�q�����פJ
====================================
type:section

- Open Data
- XML �i�����аO���y��
- �������� Webscraping
- API (Application programming interfaces)
- JSON�榡�ɮ�

Open Data �}����
====================================
type:sub-section
- 2011�~���ʶ}��F���P�}���� ([����ʬ�](https://zh.wikipedia.org/wiki/%E9%96%8B%E6%94%BE%E8%B3%87%E6%96%99))
- �����ۧ@�v�B�M�Q�v�A�H�Ψ�L�޲z����ҭ���A����H���i�H�ۥѥX���ϥ�
- �`�����x�s�覡��: 
    - `CSV`
    - `JSON`
    - `XML`
    
Open Data �}���Ʊ`�����x
====================================
- [�F����ƶ}�񥭥x](http://data.gov.tw/)
- [Data Taipei](http://data.taipei/)
- [�}���� x �}����](http://data.tycg.gov.tw/)
- [���F��ƶ}�񥭥x](http://data.moi.gov.tw/)

XML �i�����аO���y��
====================================
type:sub-section

- E**x**tensible **m**arkup **l**anguage
- �y�z**���c��**��ƪ��y��
- �B�zXML�ɮ׬O����**Html**���Ϊ���¦
- Components
    - Markup �аO - labels that give the text structure
    - Content ���� - the actual text of the document
- [XML Wiki](https://zh.wikipedia.org/wiki/XML)

XML �i�����аO���y��
====================================
Tags, elements and attributes

- Tags correspond to general labels
    - Start tags `<breakfast_menu>`, `<price>`
    - End tags `</breakfast_menu>`,`</price>`
    - Empty tags `<line-break />`
- Elements are specific examples of tags
    - `<name>Belgian Waffles</name>`
- Attributes are components of the label
    - `<book category="web">`
    
XML �i�����аO���y��-Ū��
====================================
- [�Ů�~�����(AQI)](https://data.epa.gov.tw/api/v1/aqx_p_432?limit=1000&api_key=9be7b239-557b-4c10-9775-78cadfc555e9&format=xml)
- �w��`xml2` package
- `xmlParse()`��ƱNXML�ɮ׶פJ


```r
library(xml2)
AQIURL<-"https://data.epa.gov.tw/api/v1/aqx_p_432?limit=1000&api_key=9be7b239-557b-4c10-9775-78cadfc555e9&format=xml"
AQIXML <- read_xml(AQIURL)
```

xpath?
====================================
- XML���|�y���]XML Path Language�^
- ���XML���𪬵��c�A���Ѧb��Ƶ��c�𤤧�M�`�I����O
- [����ʬ�](https://zh.wikipedia.org/wiki/XPath)
- [�`���y�k](http://tech-marsw.logdown.com/blog/2016/01/11/parsing-lxml-xpath-sheet)

XML �i�����аO���y��-�ѪR
====================================
�ϥ�`xml_find_all()`�H��`xml_text()`��ƨ��o���w���Ҥ������

```r
#���o�Ҧ�"code_name"���Ҥ������
code_name_xml<-xml_find_all(AQIXML, ".//SiteName")
code_name<-xml_text(code_name_xml)
code_name[1:10]
```

```
 [1] "��" "����" "�U��" "�s��" "�g��" "�O��" "�s��" "��d" "�L�f" "�H��"
```

XML �i�����аO���y��-�ѪR
====================================
�ϥ�`xml_find_all()`�H��`xml_text()`��ƨ��o���w���Ҥ������

```r
#���o�U�ʴ������g��longitude
longitude_xml<-xml_find_all(AQIXML, ".//Longitude")
longitude<-xml_text(longitude_xml)
longitude[1:10]
```

```
 [1] "121.760056" "121.6423"   "121.689881" "121.537778" "121.451861"
 [6] "121.458667" "121.4325"   "121.481028" "121.376869" "121.449239"
```

XML�ɮ׶פJ�m��
====================================
type:alert
incremental:true
- ���J[�A���~����污](https://data.coa.gov.tw/Service/OpenData/FromM/FarmTransData.aspx?FOTT=Xml)
- ���ը��o�U��������@���W�ٻP������
- �Ѧҭ�誺AQI�d��

```r
library(xml2)
AQIURL<-"https://data.epa.gov.tw/api/v1/aqx_p_432?limit=1000&api_key=9be7b239-557b-4c10-9775-78cadfc555e9&format=xml"
AQIXML <- read_xml(AQIURL)
code_name_xml<-xml_find_all(AQIXML, ".//SiteName")
code_name<-xml_text(code_name_xml)
code_name[1:10]
```



API
====================================
type:sub-section
- ���ε{������
- **A**pplication **P**rogramming **I**nterfaces
- ���F���ĤT�誺�}�o�̥i�H�B�~�}�o���ε{���ӱj�ƥL�̪����~�A���X�i�H�P�t�η��q������
- ��API���U�i�N����^���L�{�۰ʤ�
    -  �H�U��Open Data���ҡA�Y�ɮק�s�W�c�A�ϥΤ�ʤU���۷�Ӯ�
- [����ʬ�](https://zh.wikipedia.org/zh-tw/%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E6%8E%A5%E5%8F%A3)

API - Open Data
====================================
- [��餽�@�ۦ樮�Y�ɪA�ȸ��](http://data.tycg.gov.tw/opendata/datalist/datasetMeta?oid=5ca2bfc7-9ace-4719-88ae-4034b9a5a55c)���
- �C���s
- ���i��C���ʤU��
- ���ѳz�L**API**�U�����A��
- �z�LAPI�U������Ʈ榡: **JSON�榡**

***

- [��餽�@�ۦ樮�Y�ɪA�ȸ��API��T](http://data.tycg.gov.tw/opendata/datalist/datasetMeta/outboundDesc?id=5ca2bfc7-9ace-4719-88ae-4034b9a5a55c&rid=a1b4714b-3b75-4ff8-a8f2-cc377e4eaa0f)
    - **��ƶ�ID**: ������ƪ��򥻰ѼơA�p�]�t���B��s�W�v��
    - **���RID**: ��ƶ�
    - �^���d��


JSON�榡�ɮ�
====================================
type:sub-section

- JSON (**J**ava**s**cript **O**bject **N**otation)
- ���q�Ū���ƥ洫�y��
- From **a**pplication **p**rogramming **i**nterfaces (APIs)
- JavaScript�BJava�BNode.js����
- �@��NoSQL��Ʈw��JSON�x�s��ơG**MongoDB**
- [Wiki](http://en.wikipedia.org/wiki/JSON)


JSON�ɮ׶פJ
====================================
- `jsonlite` package (�M��ϥΫe�����w��)
- `fromJSON()`��Ƹ��JJSON���
- �p�GAPI���}��**https**�A�h�ݨϥ� `httr` package
    - �ϥ�`GET()`��ƳB�z����^�����}
- API���}�Ѧ�[��餽�@�ۦ樮�Y�ɪA�ȸ��API��T](http://data.tycg.gov.tw/opendata/datalist/datasetMeta/outboundDesc?id=5ca2bfc7-9ace-4719-88ae-4034b9a5a55c&rid=a1b4714b-3b75-4ff8-a8f2-cc377e4eaa0f)

```r
library(jsonlite)
library(RCurl)
APIData<-fromJSON("http://data.tycg.gov.tw/api/v1/rest/datastore/a1b4714b-3b75-4ff8-a8f2-cc377e4eaa0f?format=json")
```

JSON�ɮ׶פJ
====================================
- ��s��`�C��list`�����A
- ��Ӥl����(success, result)
- result��records�l���������O����Ʈ�data.frame

```r
str(APIData)
```

```
List of 2
 $ success: logi TRUE
 $ result :List of 8
  ..$ include_total : logi TRUE
  ..$ resource_id   : chr "a1b4714b-3b75-4ff8-a8f2-cc377e4eaa0f"
  ..$ fields        :'data.frame':	15 obs. of  2 variables:
  .. ..$ type: chr [1:15] "int" "text" "text" "text" ...
  .. ..$ id  : chr [1:15] "_id" "sno" "sna" "tot" ...
  ..$ records_format: chr "objects"
  ..$ records       :'data.frame':	100 obs. of  15 variables:
  .. ..$ _id    : int [1:100] 1 2 3 4 5 6 7 8 9 10 ...
  .. ..$ sno    : chr [1:100] "2001" "2002" "2003" "2004" ...
  .. ..$ sna    : chr [1:100] "�����j�ǹϮ��]" "���c����" "��������(������)" "���c������(�e��)" ...
  .. ..$ tot    : chr [1:100] "60" "52" "54" "114" ...
  .. ..$ sbi    : chr [1:100] "37" "33" "24" "70" ...
  .. ..$ sarea  : chr [1:100] "���c��" "���c��" "���c��" "���c��" ...
  .. ..$ mday   : chr [1:100] "20201113171816" "20201113171842" "20201113171827" "20201113171825" ...
  .. ..$ lat    : chr [1:100] "24.968128" "24.960815" "24.959113" "24.953874" ...
  .. ..$ lng    : chr [1:100] "121.194666" "121.212038" "121.224805" "121.2256" ...
  .. ..$ ar     : chr [1:100] "���j��300��(�����j�Ǯդ��Ϯ��]�e)" "��������G�q215���ﭱ�H��D" "������101-113���ﭱ�H��D" "���M��139���ﭱ����" ...
  .. ..$ sareaen: chr [1:100] "Zhongli Dist." "Zhongli Dist." "Zhongli Dist." "Zhongli Dist." ...
  .. ..$ snaen  : chr [1:100] "National Central University Library" "Jhungli Senior High School" "Zhongzheng Park (Zhongmei Rd.)" "TRA Zhongli Station (Front)" ...
  .. ..$ aren   : chr [1:100] "No.300, Zhongda Rd." "No.215, Sec. 2, Zhongyang W. Rd. (opposite)" "No.101 to No.113, Zhongmei Rd. (opposite)" "No.139, Zhonghe Rd. (opposite)" ...
  .. ..$ bemp   : chr [1:100] "22" "19" "29" "44" ...
  .. ..$ act    : chr [1:100] "1" "1" "1" "1" ...
  ..$ offset        : int 0
  ..$ total         : int 363
  ..$ limit         : int 100
```

JSON�ɮ׸ѪR
====================================
- �ϥ�`$`�Ÿ��I�������P�l����

```r
head(APIData$result$records)
```

| _id|sno  |sna              |tot |sbi |sarea  |mday           |lat       |lng        |
|---:|:----|:----------------|:---|:---|:------|:--------------|:---------|:----------|
|   1|2001 |�����j�ǹϮ��]   |60  |37  |���c�� |20201113171816 |24.968128 |121.194666 |
|   2|2002 |���c����         |52  |33  |���c�� |20201113171842 |24.960815 |121.212038 |
|   3|2003 |��������(������) |54  |24  |���c�� |20201113171827 |24.959113 |121.224805 |
|   4|2004 |���c������(�e��) |114 |70  |���c�� |20201113171825 |24.953874 |121.2256   |
|   5|2005 |����j��         |82  |21  |���c�� |20201113171826 |24.957943 |121.240201 |
|   6|2006 |�Ȫe�s��         |58  |27  |���c�� |20201113171837 |24.961716 |121.224241 |
|   7|2007 |���c�Ϥ���       |40  |14  |���c�� |20201113171827 |24.965697 |121.224696 |
|   8|2008 |��������         |96  |60  |���c�� |20201113171839 |24.962812 |121.217385 |

JSON�ɮ׸ѪR
====================================
���R�U��**�a��**������

```r
table(APIData$result$records$sarea)
```

|Var1   | Freq|
|:------|----:|
|�K�w�� |    5|
|�j��� |    2|
|�j�˰� |    2|
|���c�� |   35|
|����� |    7|
|���� |   32|
|�t�s�� |   10|
|Ī�˰� |    7|
���R�i�����c�Ϩ������h


JSON�ɮ׶פJ�m��
====================================
type:alert
incremental:true

- �m�ߥθ�ơG[�u�Ů�~���ơvAPI�s��](https://data.epa.gov.tw/api/v1/aqx_p_432?limit=1000&api_key=9be7b239-557b-4c10-9775-78cadfc555e9&format=json)
- �ϥ��ɮ׶פJ**�d��**�A�N��ƶפJR��
    - ���ܡG**fromJSON**
- �ϥ�str()����[��פJ�����
- �аݦ��X���[��ȡH�X�����H


�������� Webscraping
====================================
type:sub-section

- ���O�C�Ӻ���������API
- �H�u�ƻs�K�W?!
- �{���ƪ��覡�^���������: **�������Ρ]Webscraping�^**�][Webscraping Wiki](http://en.wikipedia.org/wiki/Web_scraping)�^
- �i��ӶO�ܦh�����y�q�M�귽 �Ыܥi��Q��IP
- �bR���B�z��k
    - ��@XML�ɮ׳B�z���R
    - �ϥ�`rvest` package���U

�������� Webscraping-rvest
====================================

���J[rvest](https://github.com/hadley/rvest)�M���A�g�ѥH�U�B�J�i������ѪR�G

- �ϥ�`read_html(�����^�����������}��)`���Ū������
- �ϥ�`html_nodes()`����^���һݤ��e (����CSS��xpath����)
- �ϥ�`html_text()`��ƳB�z/�M�~�^�����e�A�d�U�ݭn�����
- �ϥ�`html_attr()`����^����ưѼơ]�p�s��url�^

�������� Webscraping-rvest
====================================

```r
library(rvest) ##���J
Repoterurl<-"https://www.twreporter.org/topics"
Repoterhtml<-read_html(Repoterurl)
news_title <- Repoterhtml %>% 
    html_nodes(".kmupWO") %>% html_text()
news_title
```

```
[1] "����57�U�̦n���ɥ��G�I�G�@�ɪ��q�v��"      
[2] "�j���U���t�~�w�w�I�t�������˪����Ƿ~���N�C�~"
[3] "��H���x�i�榡�w�w��������U���x��s�a��"    
[4] "���O���Y�ɥN"                              
[5] "�a�����K�D�w�w�n�K�F�������v�P�p�v�ԧ�"      
```


�������� Webscraping-rvest
====================================
- �^�����󪺼��g�|�]�����y�k���P�Ӧ��t��
- �ϥ�**Google Chrome�}�o�u��**���U�[���^����ƪ�����
    - �Ψϥ�**SelectorGadget**���U
    - �Ψϥ�**xpath-helper**���Uxpath���Ҫ��^��
- �[��ݭn�^������ƩҦbHTML���q
    - css class��`.kmupWO`



�L���`�̪Ѹ�ƪ��� -1
====================================
[�s�Ѹ��](https://fubon-ebrokerdj.fbs.com.tw/z/ze/zeg/zega_EBTW50E_I.djhtm)

```r
library(rvest) 
NanoStockUrl<-"https://fubon-ebrokerdj.fbs.com.tw/z/ze/zeg/zega_EBTW50E_I.djhtm"
NanoStockContent<-read_html(NanoStockUrl)
NanoStockName<-
  NanoStockContent %>% html_nodes("#oAddCheckbox") %>% 
    html_text()
NanoStockPrice<-
  NanoStockContent %>% html_nodes(".t3n1")%>% 
    html_text()

head(NanoStockName)
```

```
[1] "\r\n\r\n<!--\r\n\tGenLink2stk('AS1101','�x�d');\r\n//-->\r\n"
[2] "\r\n\r\n<!--\r\n\tGenLink2stk('AS1102','�Ȫd');\r\n//-->\r\n"
[3] "\r\n\r\n<!--\r\n\tGenLink2stk('AS1216','�Τ@');\r\n//-->\r\n"
[4] "\r\n\r\n<!--\r\n\tGenLink2stk('AS1301','�x��');\r\n//-->\r\n"
[5] "\r\n\r\n<!--\r\n\tGenLink2stk('AS1303','�n��');\r\n//-->\r\n"
[6] "\r\n\r\n<!--\r\n\tGenLink2stk('AS1326','�x��');\r\n//-->\r\n"
```

```r
head(NanoStockPrice)
```

```
[1] "42.45"     "29,451"    "60"        "42.30"     "11,868"    "1,248,911"
```

�L���`�̪Ѹ�ƪ��� -2
====================================

```r
NanoStockPriceTable<-
  matrix(NanoStockPrice,ncol=6, byrow=TRUE)
NanoStockNameClean<-gsub('\\r|<|!|\\n|\\t|GenLink2stk|;|/|-|>',
                         '',
                         NanoStockName)
NanoStockData <- 
    data.frame(name = NanoStockNameClean,
               NanoStockPriceTable)
```

�L���`�̪Ѹ�ƪ��� -3
====================================

```r
NanoStockData
```

|name                    |X1       |X2      |X3 |X4       |X5     |X6         |
|:-----------------------|:--------|:-------|:--|:--------|:------|:----------|
|('AS1101','�x�d')       |42.45    |29,451  |60 |42.30    |11,868 |1,248,911  |
|('AS1102','�Ȫd')       |43.60    |5,932   |22 |43.55    |3,343  |256,638    |
|('AS1216','�Τ@')       |68.20    |34,573  |80 |68.20    |11,481 |2,344,874  |
|('AS1301','�x��')       |87.00    |18,749  |65 |87.00    |11,428 |1,629,994  |
|('AS1303','�n��')       |63.90    |4,677   |29 |64.10    |6,811  |299,760    |
|('AS1326','�x��')       |76.90    |9,903   |44 |76.90    |6,823  |759,500    |
|('AS1402','���F�s')     |27.55    |8,465   |33 |27.50    |2,263  |231,277    |
|('AS2002','����')       |21.50    |39,073  |72 |21.50    |28,552 |840,156    |
|('AS2105','���s')       |40.00    |11,227  |33 |39.90    |4,121  |455,265    |
|('AS2207','�M����')     |665.00   |1,001   |28 |664.00   |317    |664,230    |
|('AS2301','���_��')     |47.30    |4,628   |30 |47.05    |7,021  |218,987    |
|('AS2303','�p�q')       |31.20    |31,418  |73 |31.20    |31,652 |978,364    |
|('AS2308','�x�F�q')     |200.00   |9,714   |63 |200.00   |5,335  |1,940,989  |
|('AS2317','�E��')       |81.50    |95,844  |86 |81.40    |58,345 |7,813,860  |
|('AS2327','�ꥨ')       |398.00   |18,458  |76 |397.00   |8,029  |7,349,863  |
|('AS2330','�x�n�q')     |460.50   |208,443 |88 |462.00   |64,438 |95,799,486 |
|('AS2357','�غ�')       |247.50   |6,644   |59 |247.00   |3,063  |1,640,463  |
|('AS2379','��R')       |362.00   |9,396   |62 |363.00   |3,045  |3,376,136  |
|('AS2382','�s�F')       |71.80    |7,159   |41 |71.90    |3,363  |512,143    |
|('AS2395','���')       |294.50   |294     |15 |294.50   |2,125  |86,666     |
|('AS2408','�n�Ȭ�')     |62.00    |7,164   |34 |61.90    |3,167  |443,240    |
|('AS2412','���عq')     |110.00   |10,030  |54 |110.00   |6,826  |1,099,711  |
|('AS2454','�p�o��')     |675.00   |29,730  |86 |679.00   |4,318  |19,977,552 |
|('AS2474','�i��')       |191.50   |7,961   |46 |192.00   |1,860  |1,518,117  |
|('AS2633','�x�W���K')   |31.35    |3,986   |28 |31.40    |2,992  |125,271    |
|('AS2801','����')       |17.85    |6,981   |33 |17.90    |13,740 |124,465    |
|('AS2880','�ثn��')     |18.30    |37,000  |63 |18.30    |22,983 |675,701    |
|('AS2881','�I����')     |45.10    |18,654  |47 |45.20    |10,525 |842,604    |
|('AS2882','�����')     |40.50    |12,286  |54 |40.45    |12,168 |497,911    |
|('AS2883','�}�o��')     |8.65     |9,897   |45 |8.64     |12,712 |85,625     |
|('AS2884','�ɤs��')     |26.10    |72,785  |84 |26.10    |46,633 |1,896,328  |
|('AS2885','���j��')     |18.55    |37,365  |71 |18.55    |15,642 |694,888    |
|('AS2886','���ת�')     |29.35    |26,093  |68 |29.35    |20,033 |762,997    |
|('AS2887','�x�s��')     |13.20    |25,588  |62 |13.20    |27,905 |337,234    |
|('AS2890','���ת�')     |11.20    |15,626  |41 |11.15    |13,721 |174,851    |
|('AS2891','���H��')     |19.55    |29,974  |64 |19.55    |17,302 |586,010    |
|('AS2892','�Ĥ@��')     |21.45    |37,130  |73 |21.50    |29,589 |795,075    |
|('AS2912','�Τ@�W')     |269.50   |7,676   |60 |270.00   |2,338  |2,072,024  |
|('AS3008','�j�ߥ�')     |3,380.00 |15,707  |88 |3,370.00 |2,324  |52,457,395 |
|('AS3045','�x�W�j')     |99.30    |14,168  |43 |99.40    |4,096  |1,409,352  |
|('AS3711','�����뱱') |70.80    |21,422  |69 |70.50    |10,669 |1,513,632  |
|('AS4904','����')       |61.20    |6,609   |34 |61.50    |1,676  |405,508    |
|('AS4938','�M��')       |63.90    |23,800  |68 |64.10    |7,370  |1,519,697  |
|('AS5871','����KY')     |158.00   |21,138  |77 |158.50   |8,512  |3,338,554  |
|('AS5876','�W���ӻ�')   |40.00    |4,231   |21 |40.10    |1,659  |170,285    |
|('AS5880','�X�w��')     |20.15    |26,341  |62 |20.20    |31,724 |530,954    |
|('AS6415','���OKY')     |2,140.00 |526     |35 |2,085.00 |916    |1,137,705  |
|('AS6505','�x���')     |91.60    |7,592   |45 |92.00    |3,881  |692,291    |
|('AS6669','�n�o')       |707.00   |10,529  |64 |710.00   |1,276  |7,373,794  |
|('AS9910','�׮�')       |186.50   |4,526   |30 |186.00   |2,918  |843,141    |

    
���νm��
====================================
type:alert

- [Ptt Tech_Job ��](https://www.ptt.cc/bbs/Tech_Job/index.html)
- �յ۪��X�Ҧ�**���D**
- ���X���ĤT�Ӽ��D�O�H


�������� �A�Q�Q�H
====================================
incremental:true

- ���... �ܦh��Ʀ���L�s���覡�A��API
    - https://www.dcard.tw/_api/forums/cgu/posts
    - https://www.dcard.tw/_api/posts/225917717
    - https://www.dcard.tw/_api/posts/225917717/comments
- ���p���D �]OkCupid�ƥ�^
    - [70,000 OkCupid Users Just Had Their Data Published](https://motherboard.vice.com/en_us/article/70000-okcupid-users-just-had-their-data-published)

�i������
====================================
- CSS Selector �y�k���� [�ѦҸ��](https://www.w3schools.com/cssref/css_selectors.asp)
    - **.**xxx�Gselect elements with class="xxx"
    - **#**xxx�Gselect elements with id="xxx"
    - **[**yyy**]**�Gselect elements with attribute yyy
    - **[**yyy=zzz**]**�Gselect elements with attribute yyy="zzz"
    
- �r������������
    - �[��Google Chrome �}�o�̤u��A�bNetwork�����api�I�s�覡
    - �f�t�ϥ�RSelenium �����s�����A [DCard��@R Code](https://github.com/CGUIM-BigDataAnalysis/BigDataCGUIM/blob/master/105/RSelenium_rvest.md)


��L���ά����ѦҸ귽
====================================
- [�������ι�@ - �� r �y�����y�ۤv�����ε{��](https://www.slideshare.net/secret/mdfHLPgvIW1kPR)
- [rvest GitHub](https://github.com/hadley/rvest)
- R Bloggers ���ܦh[���νd��](http://www.r-bloggers.com/?s=Web+Scraping)�]�^��^
- [Ptt���ι�@](http://bryannotes.blogspot.tw/2014/08/r-ptt-wantedsocial-network-analysis.html)
- [�j�ƾǰ� �������νҵ{](http://www.largitdata.com/course_list/1)


�qFacebook�פJ
====================================
type:section
- Graph API in R
- Rfacebook package

Graph API in R
====================================
type:sub-section

- �b2018�~�����i��AGraph API�Y�n�Φb�������}���M�A���g�LFB�f��
- [Graph API](https://developers.facebook.com/docs/graph-api?locale=zh_TW)
    - �ھڿz�����A�^��JSON�榡�����
- [Graph API Explorer](https://developers.facebook.com/tools/explorer/)
    - ���ո�Ƽ�����k�M���G
- �����n���o�ۤv��**access token** (�s���v��)
    - �i�b[Graph API Explorer](https://developers.facebook.com/tools/explorer/)�����k�W����**Get Token**���s���o
    - [�x����](https://developers.facebook.com/docs/facebook-login/access-tokens/?locale=zh_TW)


Rfacebook package
====================================
type:sub-section
�b2018�~�����i��AGraph API�Y�n�Φb�������}���M�A���g�LFB�f�֡A�]�����ҵ{�ثe�L�k�ܽd�����M������

�ϥ� Rfacebook ���o `tsaiingwen` �����������

```r
library(Rfacebook) #�즸�ϥζ����w��
token<-"your token" #�Ntoken�ƻs�즹�B
getPage("tsaiingwen", token,n = 5)
```
�Y�g�L�f�֡A�i�o�U�C���G

```
4 posts       from_id           from_name
1 46251501064 ���^�� Tsai Ing-wen
2 46251501064 ���^�� Tsai Ing-wen
3 46251501064 ���^�� Tsai Ing-wen
4 46251501064 ���^�� Tsai Ing-wen
```

�qTwitter�פJ
====================================
type:section
- Twitter API
- rtweet package

Twitter API
====================================
- https://developer.twitter.com/en/apps
- �ݦ�Twitter�b���óq�L�}�o�̼f��

rtweet package
====================================

```r
## install rtweet from CRAN
install.packages("rtweet")
## load rtweet package
library(rtweet)
```

rtweet package - token �]�w
====================================

```r
library(rtweet)
create_token(
  app = "teach0309",
  consumer_key = "Wbba6ysyPKGstGAqohmtyWZOE",
  consumer_secret = "GJweDzVvXGrbjz26bHTr3d6dFI7q9gFCH98f3Ct2yk3APPWigc",
  access_token = "216362944-VbXiYOjGtENwSI6eJ9AoDK5OVvoQWlj7yIeXraGt",
  access_secret = "jnfDCvuMdxdmxswUUPPi3gomxIWZq3BTdumykLJb7GW5A")
```

```
<Token>
<oauth_endpoint>
 request:   https://api.twitter.com/oauth/request_token
 authorize: https://api.twitter.com/oauth/authenticate
 access:    https://api.twitter.com/oauth/access_token
<oauth_app> teach0309
  key:    Wbba6ysyPKGstGAqohmtyWZOE
  secret: <hidden>
<credentials> oauth_token, oauth_token_secret
---
```

rtweet package - �j�Mhashtag
====================================

```r
## search for 3000 tweets using the trump hashtag
rt <- search_tweets(
  "#trump", n = 3000, include_rts = FALSE
)
head(rt)
```




























































































































```
processing file: EMBA_PipelinesForDataAnalysisInR2.Rpres

Attaching package: 'rtweet'

The following object is masked from 'package:jsonlite':

    flatten

Requesting token on behalf of user...
Quitting from lines 512-516 (EMBA_PipelinesForDataAnalysisInR2.Rpres) 
���~: API user token required. see http://rtweet.info/articles/auth.html for instructions
���~: Warning messages:
1: package 'xml2' was built under R version 4.0.2 
2: package 'rtweet' was built under R version 4.0.3 
�������
```
