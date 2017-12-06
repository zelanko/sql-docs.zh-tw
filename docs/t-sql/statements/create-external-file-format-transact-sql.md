---
title: "建立外部檔案格式 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL FILE FORMAT
- CREATE_EXTERNAL_FILE_FORMAT
dev_langs: TSQL
helpviewer_keywords:
- External
- External, file format
- PolyBase, external file format
ms.assetid: abd5ec8c-1a0e-4d38-a374-8ce3401bc60c
caps.latest.revision: "25"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6db9730d5e0905d464a57151365a9413f61a86eb
ms.sourcegitcommit: 16347f3f5ed110b5ce4cc47e6ac52b880eba9f5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="create-external-file-format-transact-sql"></a>建立外部檔案格式 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  建立 PolyBase 外部檔案格式定義為外部資料儲存在 Hadoop、 Azure blob 儲存體或 Azure 資料湖存放區。 建立外部檔案格式是建立 PolyBase 的外部資料表的必要元件。 藉由建立外部檔案格式，您可以指定將外部資料表所參考的資料的實際配置。  
  
 PolyBase 支援這些檔案格式：  
  
-   分隔的文字檔  
  
-   RCFile hive 控制檔  
  
-   ORC hive 控制檔  
  
-   Parquet  
  
 若要建立外部資料表，請參閱[CREATE EXTERNAL TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-table-transact-sql.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Create an external file format for PARQUET files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = PARQUET  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.GzipCodec'      }  
    ]);  
  
--Create an external file format for ORC files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = ORC  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.DefaultCodec'      }  
    ]);  
  
--Create an external file format for RCFILE.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = {  
        'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
      | 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'  
    }  
    [ , DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec' ]);  
  
--Create an external file format for DELIMITED TEXT files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT  
    [ , FORMAT_OPTIONS ( <format_options> [ ,...n  ] ) ]  
    [ , DATA_COMPRESSION = {  
           'org.apache.hadoop.io.compress.GzipCodec'  
         | 'org.apache.hadoop.io.compress.DefaultCodec'  
        }  
     ]);  
  
<format_options> ::=  
{  
    FIELD_TERMINATOR = field_terminator  
    | STRING_DELIMITER = string_delimiter  
    | DATE_FORMAT = datetime_format  
    | USE_TYPE_DEFAULT = { TRUE | FALSE } 
    | Encoding = {'UTF8' | 'UTF16'} 
}  
```  
  
## <a name="arguments"></a>引數  
 *file_format_name*  
 指定外部檔案格式的名稱。  
  
 FORMAT_TYPE  
 指定外部資料的格式。  
  
 PARQUET  
 指定 Parquet 格式。  
  
 ORC  
 指定最佳化的資料列單欄式 (ORC) 格式。 此選項需要 Hive 0.11 或外部的 Hadoop 叢集上更高版本。 在 Hadoop，ORC 檔案格式會提供更好的壓縮和效能比 RCFILE 檔案格式。  
  
 RCFILE (搭配 SERDE_METHOD = *SERDE_method*)  
 指定記錄單欄式檔案格式 (RcFile)。 此選項需要您指定的 hive 控制檔的序列化和還原序列化程式 (SerDe) 方法。 如果您使用 Hadoop Hive/HiveQL 查詢 RC 檔，這項需求都相同。 請注意，SerDe method 是區分大小寫。  
  
 使用 PolyBase 支援兩種 SerDe 方法指定 RCFile 範例。  
  
-   FORMAT_TYPE = RCFILE，SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
  
-   FORMAT_TYPE = RCFILE，SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'  
  
 DELIMITEDTEXT  
 指定以文字格式的資料行分隔符號，也稱為欄位結束字元。  
  
 FIELD_TERMINATOR = *field_terminator*  
 僅適用於分隔的文字檔。 這會指定標記的每個欄位 （資料行） 結尾的一或多個字元的文字分隔檔案中。 預設值是管道字元 ꞌ | ꞌ。 如需保證支援，我們建議使用一或多個 ascii 字元。
  
  
 範例:  
  
-   FIELD_TERMINATOR = ' |'  
  
-   FIELD_TERMINATOR = ' '  
  
-   FIELD_TERMINATOR = ꞌ\tꞌ  
  
-   FIELD_TERMINATOR = ' ~ | ~'  
  
 STRING_DELIMITER = *string_delimiter*  
 文字分隔檔案中指定之資料的字串類型的欄位結束字元。 字串分隔符號的長度的一或多個字元，且括在單引號。 預設為空字串""。 如需保證支援，我們建議使用一或多個 ascii 字元。
 
  
 範例:  

-   STRING_DELIMITER = '"'

-   STRING_DELIMITER = '0x22'-雙引號括住的十六進位
  
-   STRING_DELIMITER = ' *'  
  
-   STRING_DELIMITER = Ꞌ，Ꞌ  
  
-   STRING_DELIMITER = '0x7E0x7E'-兩個 tildas (例如 ~ ~)
  
 DATE_FORMAT = *fieldinfo*  
 指定自訂格式，可能會出現文字分隔的檔案中的所有日期和時間資料。 如果原始程式檔會使用預設的日期時間格式，不需要這個選項。 只有一個自訂的日期時間格式允許每個檔案。 您無法指定每個檔案的多個自訂日期時間格式。 不過，您可以使用多個日期時間格式，如果每個外部資料表定義中其各自的資料類型的預設格式。
 
 
PolyBase 只會使用自訂日期格式匯入資料。 它不使用自訂格式以將資料寫入至外部檔案。

 當 DATE_FORMAT 未指定，或為空字串時，PolyBase 將使用下列的預設格式：  
  
-   日期時間: ' yyyy-MM-dd hh: mm: '  
  
-   SmallDateTime: ' yyyy-MM-dd hh: mm '  
  
-   日期: ' yyyy-MM-dd'  
  
-   DateTime2: ' yyyy-MM-dd hh: mm: '  
  
-   DateTimeOffset: ' yyyy-MM-dd hh: mm: '  
  
-   時間: ' ss '  
  
 **範例日期格式**下表中。  
  
 資料表的相關注意事項：  
  
-   年、 月和日可以有各種不同的格式和訂單。 下表只會顯示 ymd。 月份可以有 1 或 2 的數字，或是 3 個字元。 日期可以有 1 或 2 位數。 年份可以有 2 或 4 位數。  
  
-   毫秒 (fffffff) 則不需要。  
  
-   Am，pm (tt) 不需要。 預設為 AM。  
  
|Date 類型|範例|Description|  
|---------------|-------------|-----------------|  
|DateTime|DATE_FORMAT = 'yyyy MM dd HH:mm:ss.fff'|除了 年、 月、 日，這包括 00-24 小時，00-59 分鐘、 00-59 秒，而 3 位數 （毫秒）。|  
|DateTime|DATE_FORMAT = 'yyyy MM dd hh:mm:ss.ffftt'|除了 年、 月、 日，這包括 00-12 小時，00-59 分鐘、 00-59 秒、 毫秒和 AM，3 位數 am、 PM、 或 pm。|  
|SmallDateTime|DATE_FORMAT = ' yyyy-MM-dd hh: mm '|除了 年、 月和日，這包括 00-23 小時，00-59 分鐘的時間。|  
|SmallDateTime|DATE_FORMAT = 'yyyy MM dd hh:mmtt'|除了 年、 月和日，這包括 00-11 小時，00-59 分鐘、 沒有秒，且 AM、 am、 PM、 或 pm。|  
|日期|DATE_FORMAT = ' yyyy-MM-dd'|年、 月和日。 沒有任何時間項目會包含項目。|  
|日期|DATE_FORMAT = ' yyyy-MMM-dd'|年、 月和日。 指定月份時，使用 3 M，輸入的值是一項或字串年 1 月、 年 2 月、 3 月、 年 4 月、 5、 6 月、 年 7 月、 年 8 月 8，9 月、 年 10 月、 年 11 月或年 12 月。|  
|datetime2|DATE_FORMAT = 'yyyy MM dd: ss.fffffff'|除了 年、 月和日，這包括 00-23 小時，00-59 分鐘、 00-59 秒，而 7 位數毫秒。|  
|datetime2|DATE_FORMAT = 'yyyy MM dd hh:mm:ss.ffffffftt'|除了 年、 月和日，這包括 00-11 個小時，00-59 分鐘、 00-59 秒、 毫秒和 AM，7 位數 am、 PM、 或 pm。|  
|DateTimeOffset|DATE_FORMAT = 'yyyy MM dd: ss.fffffff zzz'|除了 年、 月和日，這包括 00-23 小時，00-59 分鐘、 00-59 秒，而 7 位數毫秒，且您放在做為輸入檔中將時區時差 {+ &#124;-} HH:ss。 例如，不含日光節約 Los Angeles 以來節省是 8 小時 utc 值為-08:00，在輸入檔中的指定為 Los Angeles 時區。|  
|DateTimeOffset|DATE_FORMAT = 'yyyy MM dd hh:mm:ss.ffffffftt zzz'|除了 年、 月和日，這包括 00-11 個小時，00-59 分鐘、 00-59 秒、 毫秒、 （AM、 am、 PM、 或 pm），7 位數和時區時差。 請參閱先前的資料列中的描述。|  
|Time|DATE_FORMAT = 'Hh: mm:'|沒有日期值，只為 00-23 小時，00-59 分鐘和 00-59 秒。|  
  
 所有支援的日期格式：  
  
|datetime|smalldatetime|date|datetime2|datetimeoffset|  
|--------------|-------------------|----------|---------------|--------------------|  
|[[M] M]M-[d] d-[yy] yy hh: mm: [.fff]|[[M] M]M-[d] d-[yy] yy hh: mm [: 00]|[[M] M]M-[d] d-[yy] yy|[[M] M]M-[d] d-[yy] yy hh: mm: [.fffffff]|[[M] M]M-[d] d-[yy] yy hh: mm: [.fffffff] zzz|  
|[[M] M]M-[d] d-[yy] yy hh: mm: [.fff] [tt]|[[M] M]M-[d] d-[yy] yy hh: mm [: 00] [tt]||[[M] M]M-[d] d-[yy] yy hh: mm: [.fffffff] [tt]|[[M] M]M-[d] d-[yy] yy hh: mm: [.fffffff] [tt] zzz|  
|[[M] M]M [yy] yy-[d] d hh: mm: [.fff]|[[M] M]M [yy] yy-[d] d hh: mm [: 00]|[[M] M]M [yy] yy-[d] d|[[M] M]M [yy] yy-[d] d hh: mm: [.fffffff]|[[M] M]M [yy] yy-[d] d hh: mm: [.fffffff] zzz|  
|[[M] M]M-[yy] yy-[d] d hh: mm: [.fff] [tt]|[[M] M]M-[yy] yy-[d] d hh: mm [: 00] [tt]||[[M] M]M-[yy] yy-[d] d hh: mm: [.fffffff] [tt]|[[M] M]M-[yy] yy-[d] d hh: mm: [.fffffff] [tt] zzz|  
|[yy] yy-[[M] M] M-[d] d hh: mm: [.fff]|[yy] yy-[[M] M] M-[d] d hh: mm [: 00]|[yy] yy-[[M] M] M-[d] d|[yy] yy-[[M] M] M-[d] d hh: mm: [.fffffff]|[yy] yy-[[M] M] M-[d] d hh: mm: [.fffffff] zzz|  
|[yy] yy-[[M] M] M-[d] d hh: mm: [.fff] [tt]|[yy] yy-[[M] M] M-[d] d hh: mm [: 00] [tt]||[yy] yy-[[M] M] M-[d] d hh: mm: [.fffffff] [tt]|[yy] yy-[[M] M] M-[d] d hh: mm: [.fffffff] [tt] zzz|  
|[yy] yy-[d] d-[[M] M] M hh: mm: [.fff]|[yy] yy-[d] d-[[M] M] M hh: mm [: 00]|[yy] yy-d [d]-[[M] M] M|[yy] yy-[d] d-[[M] M] M hh: mm: [.fffffff]|[yy] yy-[d] d-[[M] M] M ss [.fffffff] zzz|  
|[yy] yy-[d] d-[[M] M] M hh: mm: [.fff] [tt]|[yy] yy-[d] d-[[M] M] M hh: mm [: 00] [tt]||[yy] yy-[d] d-[[M] M] M hh: mm: [.fffffff] [tt]|[yy] yy-[d] d-[[M] M] M hh: mm: [.fffffff] [tt] zzz|  
|[d] d-[[M] M] M-[yy] yy hh: mm: [.fff]|[d] d-[[M] M] M-[yy] yy hh: mm [: 00]|[d] d-[[M] M] M-[yy] yy|[d] d-[[M] M] M-[yy] yy hh: mm: [.fffffff]|[d] d-[[M] M] M-[yy] yy hh: mm: [.fffffff] zzz|  
|[d] d-[[M] M] M-[yy] yy hh: mm: [.fff] [tt]|[d] d-[[M] M] M-[yy] yy hh: mm [: 00] [tt]||[d] d-[[M] M] M-[yy] yy hh: mm: [.fffffff] [tt]|[d] d-[[M] M] M-[yy] yy hh: mm: [.fffffff] [tt] zzz|  
|[d] d-[yy] yy-[[M] M] M hh: mm: [.fff]|[d] d-[yy] yy-[[M] M] M hh: mm [: 00]|[d] d-[yy] yy-[[M] M] M|[d] d-[yy] yy-[[M] M] M hh: mm: [.fffffff]|[d] d-[yy] yy-[[M] M] M ss [.fffffff] zzz|  
|[d] d-[yy] yy-[[M] M] M hh: mm: [.fff] [tt]|[d] d-[yy] yy-[[M] M] M hh: mm [: 00] [tt]||[d] d-[yy] yy-[[M] M] M hh: mm: [.fffffff] [tt]|[d] d-[yy] yy-[[M] M] M hh: mm: [.fffffff] [tt] zzz|  
  
 詳細資料：  
  
-   若要分隔月、 日和年值，您可以使用 '-'，'/' 或 '。 '. 為了簡單起見，資料表會使用只在 '-' 分隔符號。  
  
-   若要指定文字，表示月份會使用三個或多個字元。 1 或 2 個字元的月份會解譯為數字。  
  
-   若要分隔時間值，請使用 ': ' 符號。  
  
-   以方括弧括住的字母是選擇性的。  
  
-   字母 'tt' 指定 [AM |PM | am | pm]。 AM 是預設值。 當指定 'tt' 時，小時值 (hh) 必須在 0 到 12 的範圍內。  
  
-   字母 'zzz' 指定系統的目前的時區格式的時區位移 {+ |-} HH:ss]。  
  
 USE_TYPE_DEFAULT = {TRUE |**FALSE** }  
 指定如何處理遺漏值中分隔的文字檔時 PolyBase 會從文字檔擷取資料。  
  
 TRUE  
 擷取資料時從文字檔案，儲存每個遺漏值所使用的外部資料表定義中的對應資料行的資料型別預設值。 例如，取代遺漏值：  
  
-   如果資料行定義為數值資料行，0。  
  
-   空字串""如果字串資料行的資料行。  
  
-   1900-01-01 如果資料行是日期資料行。  
  
 FALSE  
 儲存所有遺漏的值為 NULL。 會使用 NULL 這個字分隔的文字檔案中儲存任何 NULL 值將匯入，以字串 'NULL'。  
  
   編碼 = {'UTF8' |UTF16'}   
 在 Azure SQL 資料倉儲中，PolyBase 可以讀取 UTF8 及 UTF16 LE 編碼分隔的文字檔案。 在 SQL Server 和 PDW 中，PolyBase 不支援讀取 UTF16 編碼檔案。
  
 DATA_COMPRESSION = *data_compression_method*  
 指定外部資料的資料壓縮方法。 如果沒有指定 DATA_COMPRESSION，預設為未壓縮的資料。  
 才能正常運作，Gzip 壓縮檔案必須具有 「.gz"副檔名。
 
 DELIMITEDTEXT 格式類型支援這些壓縮方式：  
  
-   資料壓縮 = 'org.apache.hadoop.io.compress.DefaultCodec'  
  
-   資料壓縮 = 'org.apache.hadoop.io.compress.GzipCodec'  

 RCFILE 格式類型支援這種壓縮方式：  
  
-   資料壓縮 = 'org.apache.hadoop.io.compress.DefaultCodec'  
  
 ORC 檔案格式類型支援這些壓縮方式：  
  
-   資料壓縮 = 'org.apache.hadoop.io.compress.DefaultCodec'  
  
-   資料壓縮 = 'org.apache.hadoop.io.compress.SnappyCodec'  
  
 PARQUET 檔案格式類型支援這些壓縮方式：  
  
-   資料壓縮 = 'org.apache.hadoop.io.compress.GzipCodec'  
  
-   資料壓縮 = 'org.apache.hadoop.io.compress.SnappyCodec'  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY EXTERNAL FILE FORMAT 權限。  
  
## <a name="general-remarks"></a>一般備註  
 外部檔案格式是在資料庫範圍[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 它是在伺服器範圍[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
 格式選項都是選用的並僅適用於分隔的文字檔。  
  
 當其中一種壓縮格式儲存資料時，PolyBase 會先傳回的資料記錄之前解壓縮資料。  
  
## <a name="limitations-and-restrictions"></a>限制事項   
  
 必須支援資料列分隔符號分隔文字檔案中的 Hadoop 的 LineRecordReader 亦即它必須是 '\r'、 '\n'、 或 '\r\n'。 這些不是使用者可設定。  
  
 RCFiles，以支援 SerDe 方法的組合和支援的資料壓縮方法會在本文中先前列出。 支援所有的組合。  
  
 並行的 PolyBase 查詢的數目上限為 32。 32 個並行查詢執行時，每個查詢就可以從外部檔案的位置讀取 33,000 檔案的最大值。 根資料夾，而且每個子資料夾也算是一個檔案。 如果並行程度小於 32，外部檔案的位置可以包含多個 33,000 檔案。  
  
 由於在外部資料表中的檔案數目的限制，我們建議您在根和外部檔案位置的子資料夾中儲存小於 30,000 檔案。 此外，我們建議您保持為較小的數字的根目錄底下的子資料夾的數目。 參考太多檔案時可能會發生 Java 虛擬機器的記憶體不足例外狀況。  
  
## <a name="locking"></a>鎖定  
 外部檔案格式物件上採用共用的鎖定。  
  
## <a name="performance"></a>效能  
 使用壓縮的檔案一律會產生取捨之間的外部資料來源和 SQL Server 之間傳送較少的資料，同時提高壓縮和解壓縮資料的 CPU 使用量。  
  
 Gzip 壓縮文字檔不是可分割的圖形。 若要改善效能 Gzip 壓縮的文字檔，我們建議產生儲存在外部資料來源的相同目錄中的多個檔案。 這將允許 PolyBase 讀取及使用多個讀取器和解壓縮的處理序解壓縮更快速的資料。 壓縮檔案的理想數目是每個計算節點的資料讀取器程序的最大數目。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，資料讀取器程序的數目上限是 8 每個節點的目前版本中。 在[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，每個節點的資料讀取器程序的最大數目會因 SLO。 請參閱[Azure SQL 資料倉儲載入模式和策略](https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies/)如需詳細資訊。  
  
## <a name="examples"></a>範例  
  
### <a name="a-create-a-delimitedtext-external-file-format"></a>A. 建立 DELIMITEDTEXT 外部檔案格式  
 這個範例會建立名為外部檔案格式*textdelimited1*文字分隔檔案。 FORMAT_OPTIONS 指定將使用縱線字元分隔檔案中的欄位 ' |'。 文字檔案也會自動使用 Gzip 轉碼器壓縮。 如果未指定 DATA_COMPRESSION，文字檔案未壓縮。  
  
 分隔文字檔的資料壓縮方法可以是預設轉碼器、 'org.apache.hadoop.io.compress.DefaultCodec' 或 Gzip 轉碼器，'org.apache.hadoop.io.compress.GzipCodec'。  
  
```  
CREATE EXTERNAL FILE FORMAT textdelimited1  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT,  
    FORMAT_OPTIONS (  
        FIELD_TERMINATOR = '|',  
        DATE_FORMAT = 'MM/dd/yyyy' ),  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'  
);  
```  
  
### <a name="b-create-an-rcfile-external-file-format"></a>B. 建立 RCFile 外部檔案格式  
 這個範例會使用序列化/還原序列化方法 org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe RCFile 建立外部檔案格式。 它也會指定要使用預設的轉碼器的資料壓縮方法。 如果未指定 DATA_COMPRESSION，預設為不壓縮。  
  
```  
CREATE EXTERNAL FILE FORMAT rcfile1  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe',  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'  
);  
```  
  
### <a name="c-create-an-orc-external-file-format"></a>C. 建立 ORC 外部檔案格式  
 這個範例會建立與 org.apache.io.compress.SnappyCodec 資料壓縮方法壓縮資料 ORC 檔案的外部檔案格式。 如果未指定 DATA_COMPRESSION，預設為不壓縮。  
  
```  
CREATE EXTERNAL FILE FORMAT orcfile1  
WITH (  
    FORMAT_TYPE = ORC,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
### <a name="d-create-a-parquet-external-file-format"></a>D. 建立 PARQUET 外部檔案格式  
 這個範例會建立 Parquet 檔案可與 org.apache.io.compress.SnappyCodec 資料壓縮方法壓縮資料的外部檔案格式。 如果未指定 DATA_COMPRESSION，預設為不壓縮。  
  
```  
CREATE EXTERNAL FILE FORMAT parquetfile1  
WITH (  
    FORMAT_TYPE = PARQUET,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
## <a name="see-also"></a>請參閱  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [建立外部 TABLE AS SELECT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [建立 TABLE AS SELECT &#40;Azure SQL 資料倉儲 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [sys.external_file_formats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)  
  
  
