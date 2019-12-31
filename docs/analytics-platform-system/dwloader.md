---
title: dwloader 命令列載入器
description: dwloader 是平行處理資料倉儲（PDW）命令列工具，可將大量的資料表資料列載入至現有的資料表。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 8ea941e45f5125beed0820c5d5242b0f86073f76
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401170"
---
# <a name="dwloader-command-line-loader-for-parallel-data-warehouse"></a>平行處理資料倉儲的 dwloader 命令列載入器
**dwloader**是平行處理資料倉儲（PDW）命令列工具，可將大量的資料表資料列載入至現有的資料表。 載入資料列時，您可以將所有資料列加入至資料表的結尾（*附加模式*或*fastappend 模式*）、附加新的資料列並更新現有的資料列（*upsert 模式*），或在載入前刪除所有現有的資料列，然後將所有資料列插入空白資料表（*重載模式*）。  
  
**載入資料的進程**  
  
1.  準備來源資料。  
  
    使用您自己的 ETL 進程來建立您想要載入的來源資料。 來源資料必須格式化，才能符合目的地資料表的架構。 將來源資料儲存至一或多個文字檔，並將文本檔案複製到載入伺服器上的相同目錄中。 如需有關載入伺服器的詳細資訊，請參閱[取得和設定載入伺服器](acquire-and-configure-loading-server.md)。  
  
2.  準備載入選項。  
  
    決定您將使用的載入選項。 將載入選項儲存在設定檔中。 將配置檔案複製到載入伺服器上的本機位置。 本主題將說明**dwloader**設定選項。  
  
3.  準備載入失敗選項。  
  
    決定您希望**dwloader**如何處理無法載入的資料列。 為了執行負載， **dwloader**會先將資料載入至臨時表，然後將資料傳輸到目的地資料表。 當載入器將資料載入到臨時表時，它會追蹤無法載入的資料列數目。 例如，格式不正確的資料列將無法載入。 失敗的資料列會複製到拒絕檔案。 根據預設，除非您指定不同的拒絕閾值，否則負載會在第一次拒絕之後中止。  
  
4.  安裝**dwloader**。  
  
    如果尚未安裝 dwloader，請將它安裝到載入伺服器上。 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  執行**dwloader**。  
  
    使用適當的命令列選項，登入載入伺服器，並執行可執行檔**dwloader** 。  
  
6.  驗證結果。  
  
    您可以檢查失敗的資料列檔案（以-R 指定），以查看是否有任何資料列無法載入。 如果此檔案是空的，則所有資料列都已成功載入。 **dwloader**是交易式的，因此如果有任何步驟失敗（除了拒絕的資料列以外），所有步驟都會回復為其初始狀態。  
  
<!-- 
![Topic link icon](media/topic-link.gif "Topic_Link")[Syntax Conventions](syntax-conventions-sql-server-pdw.md)  
-->  


## <a name="syntax"></a>語法  
  
```  
dwloader.exe { -h }  
  
dwloader.exe   
    {  
        { -U login_name  -P password  }  
        | -W  
    }  
    [ -f parameter_file ]  
    [ -S target_appliance ]  
    { -T target_database_name . [ schema ] . table_name }   
    { -i source_data_location } [ <source_data_options> ]  
    { -R load_failure_file_name } [ <load_failure_options> ]  
    [ <loading_options> ]  
}  
  
<source_data_options> ::=  
{  
    [ -fh number_header_rows ]  
    [ < variable_length_column_options > | < fixed_width_column_options > ]  
    [ -D { mdy | myd | ymd | ydm | dmy | dym | custom_date_format } ]  
    [ -dt datetime_format_file ]  
}  
  
<variable_length_column_options> ::=  
{  
    [ -e character_encoding ]  
    -r row_delimiter   
    [ -s string_delimiter ]  
    -t field_delimiter   
}  
  
<fixed_width_column_options> ::=  
{  
    -w fixed_width_config_file   
    [ -e character_encoding ]   
    -r row_delimiter   
}  
  
<load_failure_options> ::=  
{  
    [ -rt { value | percentage } ]  
    [ -rv reject_value ]  
    [ -rs reject_sample_value ]  
}  
  
<loading_options> ::=  
{  
    [ -d staging_database_name ]  
    [ -M { append | fastappend | upsert -K merge_column [ ,...n ] | reload } ]  
    [ -b batchsize ]   
    [ -c ]  
    [ -E ]  
    [ -m ]  
    [ -N ]  
    [ -se ]
    [ -l ]   
}  
```  
  
## <a name="arguments"></a>引數  
**-h**  
顯示有關使用載入器的簡單說明資訊。 只有在未指定任何其他命令列參數時，才會顯示 [說明]。  
  
**-U** *login_name*  
具有適當許可權可執行負載的有效 SQL Server Authentication 登入。  
  
**-P** *密碼*  
SQL Server 驗證*login_name*的密碼。  
  
**-W**  
使用 Windows 驗證。 （不需要*login_name*或*密碼*）。 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
使用參數檔案（ *parameter_file_name*）來取代命令列參數。 *parameter_file_name*可以包含*user_name*和*password*以外的任何命令列參數。 如果在命令列和參數檔案中指定參數，命令列會覆寫 file 參數。  
  
參數檔案包含一個參數，每行沒有**-** 前置詞。  
  
範例：  
  
`rt=percentage`  
  
`rv=25`  
  
**-S** *target_appliance*  
指定將接收已載入資料的 SQL Server PDW 設備。  
  
*對於*不會連線的連線， *target_appliance*會指定為 <設備名稱>-SQLCTL01。 若要設定此命名的連線，請參閱設定不能的[網路介面卡](configure-infiniband-network-adapters.md)。  
  
若是 Ethernet 連線， *target_appliance*是控制節點叢集的 IP 位址。  
  
如果省略，dwloader 會預設為安裝 dwloader 時所指定的值。 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name。*[*架構*]。*table_name*  
目的地資料表的三部分名稱。  
  
**-I** *source_data_location*  
要載入的一個或多個來源檔案的位置。 每個原始程式檔都必須是文字檔，或是以 gzip 壓縮的文字檔。 只有一個原始檔可以壓縮到每個 gzip 檔案。  
  
若要格式化來源檔案：  
  
-   來源檔案必須根據載入選項進行格式化。  
  
-   原始程式檔中的每一行都包含一個資料表資料列的資料。 來源資料必須符合目的地資料表的架構。 資料行順序和資料類型也必須相符。 資料列中的每個欄位都代表目的地資料表中的資料行。  
  
-   根據預設，欄位是可變長度，並以分隔符號分隔。 若要指定分隔符號類型，請使用 <variable_length_column_options> 命令列選項。 若要指定固定長度欄位，請使用 <fixed_width_column_options> 命令列選項。  
  
若要指定來源資料位置：  
  
-   來源資料位置可以是網路路徑，或是載入伺服器上目錄的本機路徑。  
  
-   若要指定目錄中的所有檔案，請輸入後面接著 * 萬用字元的目錄路徑。  載入器不會從來源資料位置中的任何子目錄載入檔案。 當 gzip 檔案中存在目錄時，載入器會發生錯誤。  
  
-   若要指定目錄中的某些檔案，請使用字元和 * 萬用字元的組合。  
  
若要使用一個命令載入多個檔案：  
  
-   所有檔案都必須存在於相同的目錄中。  
  
-   這些檔案必須全部是文字檔、所有 gzip 檔案，或是文字和 gzip 檔案的組合。  
  
-   沒有任何檔案可以包含標頭資訊。  
  
-   所有檔案都必須使用相同的字元編碼類型。 請參閱-e 選項。  
  
-   所有檔案都必須載入至相同的資料表。  
  
-   所有檔案都會串連並載入，就好像它們是一個檔案一樣，而拒絕的資料列會移至單一的拒絕檔案。  
  
範例：  
  
-   -i \\\loadserver\loads\daily\\*. gz  
  
-   -i \\\loadserver\loads\daily\\* .txt  
  
-   -i \\\loadserver\loads\daily\monday. *  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\\loadserver\loads\daily\\*  
  
**-R** *load_failure_file_name*  
如果發生載入失敗， **dwloader**會儲存無法載入的資料列，而失敗會將失敗資訊描述在名為*load_failure_file_name*的檔案中。 如果此檔案已經存在，dwloader 就會覆寫現有的檔案。 當第一次失敗時，會建立*load_failure_file_name* 。 如果所有資料列都載入成功，則不會建立*load_failure_file_name* 。  
  
**-fh** *number_header_rows*  
*Source_data_file_name*開頭要忽略的行（列）數目。 預設值為 0。  
  
<variable_length_column_options>  
具有以字元分隔之可變長度資料行的*source_data_file_name*選項。 根據預設， *source_data_file_name*包含可變長度資料行中的 ASCII 字元。  
  
若是 ASCII 檔案，則會連續放置分隔符號來表示 Null。 例如，在以管道分隔的檔案（"|"）中，Null 會以 "| |" 表示。 在逗號分隔的檔案中，Null 會以 "，，" 表示。 此外，必須指定 **-E** （--emptyStringAsNull）選項。 如需-E 的詳細資訊，請參閱下面的。  
  
**-e** *character_encoding*  
指定要從資料檔案載入之資料的字元編碼類型。 選項為 ASCII （預設值）、UTF8、UTF16 或 UTF16BE，其中 UTF16 的位元組由小到大，而 UTF16BE 為 big endian。 這些選項不區分大小寫。  
  
**-t** *field_delimiter*  
資料列中每個欄位（資料行）的分隔符號。 欄位分隔符號是其中一或多個 ASCII escape 字元或 ASCII 十六進位值。  
  
|名稱|逸出字元|十六進位字元|  
|--------|--------------------|-----------------|  
|Tab 鍵|\t|0x09|  
|回車（CR）|\r|0x0d|  
|換行字元（LF）|\n|0x0a|  
|CRLF|\r\n|0x0d0x0a|  
|Comma (逗號)|','|0x2c|  
|雙引號|\\"|0x22|  
|單引號|\\'|0x27|  
  
若要在命令列上指定管道字元，請以雙引號 "|" 括住。 這可避免命令列剖析器解釋。 其他字元則以單引號括住。  
  
範例：  
  
-t "|"  
  
-t ' '  
  
-t 0x0a  
  
-t \t  
  
-t ' ~ | ~ '  
  
**-r** *row_delimiter*  
源資料檔案中每個資料列的分隔符號。 資料列分隔符號是一或多個 ASCII 值。  
  
若要指定回車（CR）、換行字元（LF）或定位字元做為分隔符號，您可以使用 escape 字元（\r、\n、\t）或其十六進位值（0x、0d、09）。 若要指定任何其他特殊字元做為分隔符號，請使用它們的十六進位值。  
  
CR + LF 的範例：  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR 的範例：  
  
-r \r  
  
-r 0x0d  
  
LF 的範例：  
  
-r \n  
  
-r 0x0a  
  
Unix 需要 LF。 Windows 需要 CR。  
  
**-s** *string_delimiter*  
文字分隔輸入檔的字串資料類型欄位的分隔符號。 字串分隔符號是一或多個 ASCII 值。  您可以將它指定為字元（例如，-s *）或十六進位值（例如，-s 0x22 代表雙引號）。  
  
範例：  
  
今日  
  
-s 0x22  
  
< fixed_width_column_options>  
具有固定長度資料行之源資料檔案的選項。 根據預設， *source_data_file_name*包含可變長度資料行中的 ASCII 字元。  
  
當-e 是 UTF8 時，不支援固定寬度資料行。  
  
**-w** *fixed_width_config_file*  
設定檔案的路徑和名稱，指定每個資料行中的字元數。 每個欄位都必須指定。  
  
這個檔案必須位於載入伺服器上。 路徑可以是 UNC、相對或絕對路徑。 *Fixed_width_config_file*中的每一行都包含一欄的名稱，以及該資料行的字元數。 每個資料行都有一行，如下所示，而且檔案中的順序必須符合目的地資料表中的順序：  
  
*column_name*=*num_chars*  
  
*column_name*=*num_chars*  
  
範例固定寬度設定檔：  
  
SalesCode = 3  
  
SalesID = 10  
  
*Source_data_file_name*中的範例行：  
  
230Shirts0056  
  
320Towels1356  
  
在上述範例中，第一個載入的資料列會有 SalesCode = ' 230 ' 和 SalesID = ' Shirts0056 '。 第二個載入的資料列會有 SalesCode = ' 320 ' 和 SaleID = ' Towels1356 '。  
  
如需如何處理固定寬度模式中的前置和尾端空格或資料類型轉換的相關資訊，請參閱[dwloader 的資料類型轉換規則](dwloader-data-type-conversion-rules.md)。  
  
**-e** *character_encoding*  
指定要從資料檔案載入之資料的字元編碼類型。 選項為 ASCII （預設值）、UTF8、UTF16 或 UTF16BE，其中 UTF16 的位元組由小到大，而 UTF16BE 為 big endian。 這些選項不區分大小寫。  
  
當-e 是 UTF8 時，不支援固定寬度資料行。  
  
**-r** *row_delimiter*  
源資料檔案中每個資料列的分隔符號。 資料列分隔符號是一或多個 ASCII 值。  
  
若要指定回車（CR）、換行字元（LF）或定位字元做為分隔符號，您可以使用 escape 字元（\r、\n、\t）或其十六進位值（0x、0d、09）。 若要指定任何其他特殊字元做為分隔符號，請使用它們的十六進位值。  
  
CR + LF 的範例：  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR 的範例：  
  
-r \r  
  
-r 0x0d  
  
LF 的範例：  
  
-r \n  
  
-r 0x0a  
  
Unix 需要 LF。 Windows 需要 CR。  
  
**-D** { **ymd** | ydm | mdy | myd | dmy |dym |*custom_date_format* }  
指定輸入檔中所有日期時間欄位的月份（m）、日期（d）和年份（y）順序。 預設順序為 ymd。 若要為相同的原始程式檔指定多個訂單格式，請使用-dt 選項。  
  
ymd |dmy  
ydm 和 dmy 允許相同的輸入格式。 兩者都允許年份在日期的開頭或結尾。 例如，針對**ydm**和**dmy**日期格式，輸入檔中可能會有2013-02-03 或02-03-2013。  
  
ydm  
您只能將格式化為 ydm 的輸入載入 datetime 和 Smalldatetime 資料類型的資料行中。 您無法將 ydm 值載入 datetime2、date 或 datetimeoffset 資料類型的資料行。  
  
mdy  
<month> <space> <day>mdy 允許<comma>。 <year>  
  
1975年1月1日 mdy 輸入資料的範例：  
  
-   1975年1月1日  
  
-   Jan 01，75  
  
-   Jan/1/75  
  
-   01011975  
  
myd  
2010年3月04日的輸入檔範例：03-2010-04、3/2010/4  
  
dym  
2010年3月04日的輸入檔範例：04-2010-03、4/2010/3  
  
*custom_date_format*  
*custom_date_format*是自訂的日期格式（例如，MM/dd/yyyy），而且包含在僅供回溯相容性之用。 dwloader 不會強制執行自訂日期格式。 相反地，當您指定自訂日期格式時， **dwloader**會將它轉換成對應的 ymd、ydm、mdy、myd、dym 或 dmy 設定。  
  
例如，如果您指定-D MM/dd/yyyy，dwloader 會預期所有的日期輸入都會以 month first、day 和 year （mdy）排序。 它不會強制執行2個字元的月份、2位數的天數，以及4位數的年份，如自訂日期格式所指定。 以下範例說明當日期格式為-D MM/dd/yyyy：01/02/2013、Jan. 02.2013、1/2/2013 時，可以在輸入檔中格式化日期的方式  
  
如需更完整的格式資訊，請參閱[dwloader 的資料類型轉換規則](dwloader-data-type-conversion-rules.md)。  
  
**-dt** *datetime_format_file*  
每個日期時間格式都指定于名為*datetime_format_file*的檔案中。 與命令列參數不同的是，包含空格的檔案參數不得以雙引號括住。 當您載入資料時，無法改變日期時間格式。 源資料檔案及其在目的地資料表中對應的資料行必須具有相同的格式。  
  
每一行都包含目的地資料表中的資料行名稱，以及它的日期時間格式。  
  
範例：  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
將包含臨時表的資料庫名稱。 預設值是使用-T 選項指定的資料庫，也就是目的地資料表的資料庫。 如需有關使用臨時資料庫的詳細資訊，請參閱[建立臨時資料庫](staging-database.md)。  
  
**-M** *load_mode_option*  
指定是否要附加、upsert 或重載資料。 預設模式為 [附加]。  
  
附加  
載入器會將資料列插入目的地資料表中現有資料列的結尾。  
  
fastappend  
載入器會直接將資料列插入目的地資料表中現有資料列的結尾，而不使用臨時表。 fastappend 需要多重交易（-m）選項。 使用 fastappend 時，不能指定臨時資料庫。 沒有 fastappend 的回復，這表示從失敗或已中止的負載復原必須由您自己的載入進程處理。  
  
upsert **-K**  *merge_column* [,.。。*n* ]  
載入器會使用 SQL Server Merge 語句來更新現有的資料列，並插入新的資料列。  
  
-K 選項會指定要作為合併依據的一或多個資料行。 這些資料行會形成一個合併索引鍵，這應該代表一個唯一的資料列。 如果合併索引鍵存在於目的地資料表中，就會更新該資料列。 如果合併索引鍵不存在於目的地資料表中，則會附加資料列。  
  
若為雜湊分散式資料表，合併索引鍵必須是或包含散發資料行。  
  
針對複寫資料表，合併索引鍵是一或多個資料行的組合。 這些資料行是根據應用程式的需求來指定。  
  
多個資料行必須以逗號分隔，且不含空格，或以空格分隔，並括在單引號中。  
  
如果來源資料表中的兩個數據列具有相符的合併索引鍵值，則其各自的資料列必須相同。  
  
刷新  
載入器會在插入來源資料之前，先截斷目的地資料表。  
  
**-b** *batchsize*  
建議僅供 Microsoft 支援服務使用， *batchsize*是 DMS 執行于計算節點上 SQL Server 實例之大量複製的 SQL Server 批次大小。  當指定*batchsize*時，SQL Server PDW 將會覆寫針對每個負載動態計算的批次載入大小。  
  
從 SQL Server 2012 PDW 開始，控制節點預設會動態計算每個負載的批次大小。 此自動計算是根據數個參數，例如記憶體大小、目標資料表類型、目標資料表架構、載入類型、檔案大小，以及使用者的資源類別。  
  
例如，如果載入模式是 FASTAPPEND，且資料表具有叢集資料行存放區索引，SQL Server PDW 預設會嘗試使用批次大小1048576，如此資料列群組就會立即關閉並載入至資料行存放區，而不需要經過差異存放區。 如果記憶體不允許批次大小為1048576，dwloader 會選擇較小的 batchsize。  
  
如果載入類型為 FASTAPPEND，則*batchsize*適用于將資料載入資料表中，否則*batchsize*適用于將資料載入至臨時表。  
  
<reject_options>  
指定選項，以決定載入器將允許的載入失敗次數。 如果載入失敗超過閾值，載入器將會停止，而且不會認可任何資料列。  
  
**-rt** { **value** | 百分比}  
指定 **-rv** *reject_value*選項中的-*reject_value*是資料列的常值數目（值）或失敗率（百分比）。 預設值為 value。  
  
[百分比] 選項是根據-rs 選項，以間隔時間進行的即時計算。  
  
例如，如果載入器嘗試載入100個數據列，而25個失敗且75成功，則失敗率為25%。  
  
**-rv** *reject_value*  
指定在暫停負載之前允許的資料列拒絕次數或百分比。 **-Rt**選項會決定*reject_value*是指資料列的數目或資料列的百分比。  
  
預設*reject_value*為0。  
  
與-rt 值搭配使用時，載入器會在拒絕的資料列計數超過 reject_value 時停止負載。  
  
當搭配-rt 百分比使用時，載入器會以間隔（-rs 選項）來計算百分比。 因此，失敗資料列的百分比可能會超過*reject_value*。  
  
**-rs** *reject_sample_size*  
與`-rt percentage`選項搭配使用，以指定增量百分比檢查。 例如，如果 reject_sample_size 是1000，載入器會在嘗試載入1000個數據列之後，計算失敗的資料列百分比。 它會在嘗試載入每個額外的1000資料列之後重新計算失敗的資料列百分比。  
  
**-c**  
移除 char、Nchar、Varchar 和 Nvarchar 欄位左側和右邊的空白字元。 將只包含空白字元的每個欄位轉換為空字串。  
  
範例：  
  
' ' 已截斷為 ' '  
  
' abc ' 已截斷為 ' abc '  
  
當-c 與-E 搭配使用時，-E 作業會先發生。 只包含空白字元的欄位會轉換成空字串，而不是 Null。  
  
**-E**  
將空字串轉換為 Null。 預設為不執行這些轉換。  
  
**-m**  
在第二個載入階段使用多交易模式;將資料從臨時表載入至分散式資料表時。  
  
使用 **-m**，SQL Server PDW 會平行執行和認可載入。 這執行的速度比預設載入模式快，但不是交易安全的。  
  
如果不是 **-m**，SQL Server PDW 會在每個計算節點內的散發中，同時在計算節點之間，執行和認可的連續載入。 這個方法比多重交易模式慢，但卻是交易安全的。  
  
**-m**對於*append*、 *reload*和*upsert*是選擇性的。  
  
fastappend 需要 **-m** 。  
  
**-m**不能與複寫的資料表一起使用。  
  
**-m**僅適用于第二個載入階段。 它並不適用于第一個載入階段;將資料載入臨時表。  
  
不會有多重交易模式的復原，這表示從失敗或已中止的負載復原必須由您自己的載入進程處理。  
  
只有在載入空白資料表時，才建議使用 **-m** ，讓您可以在不遺失資料的情況下進行復原。 若要從載入失敗復原：卸載目的地資料表、解決載入問題、重新建立目的地資料表，然後再次執行載入。  
  
**-N**  
確認目標應用裝置具有來自受信任授權單位的有效 SQL Server PDW 憑證。 使用此協助確保您的資料不會被攻擊者攔截，並傳送到未經授權的位置。 憑證必須已安裝在設備上。 安裝憑證的唯一支援方式是讓設備系統管理員使用 Configuration Manager 工具進行安裝。 如果您不確定設備是否已安裝信任的憑證，請詢問您的裝置管理員。  
  
**-se**  
略過載入空的檔案。 這也會略過解壓縮空的 gzip 檔案。

**-l**  
適用于 CU 7.4 update，指定可載入的最大資料列長度（以位元組為單位）。 有效值為介於32768和33554432之間的整數。 僅在需要載入大型資料列（大於32KB）時使用，因為這會在用戶端和伺服器上配置更多記憶體。
  
## <a name="return-code-values"></a>傳回碼值  
0（成功）或其他整數值（失敗）  
  
在命令視窗或批次檔中，使用`errorlevel`來顯示傳回碼。 例如：  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
使用 PowerShell 時，請`$LastExitCode`使用。  
  
## <a name="permissions"></a>權限  
需要目的地資料表的載入許可權和適用的許可權（INSERT、UPDATE、DELETE）。 需要在臨時資料庫上建立許可權（用於建立臨時表）。 如果未使用臨時資料庫，則必須在目的地資料庫上建立許可權。 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>一般備註  
如需使用 dwloader 載入時資料類型轉換的詳細資訊，請參閱[dwloader 的資料類型轉換規則](dwloader-data-type-conversion-rules.md)。  
  
如果參數包含一或多個空格，請將參數括在雙引號中。  
  
您應該從其安裝的位置執行載入器。 Dwloader 可執行檔會預先安裝在設備上，且位於 C:\Program Files\Microsoft SQL Server 資料 Warehouse\DWLoader 目錄中。  
  
您可以將參數檔案（-f 選項）中指定的參數指定為命令列參數，以覆寫該參數。  
  
您可以同時執行多個載入器實例。 載入器實例的最大數目已預先設定且無法變更。 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
載入的資料在設備上可能需要比來源位置更多或更少的空間。 您可以使用資料子集來執行測試匯入，以估計磁片耗用量。  
  
雖然**dwloader**是交易處理常式，而且會在失敗時正常回復，但一旦大量載入順利完成，就無法回復。 若要取消使用中的**dwloader**進程，請輸入 CTRL + C。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
同時發生的所有載入總大小必須小於資料庫的 LOG_SIZE，而且我們建議所有並行載入的總大小低於 LOG_SIZE 的50%。 若要達到這種大小限制，您可以將大型負載分割成多個批次。 如需 LOG_SIZE 的詳細資訊，請參閱[建立資料庫](../t-sql/statements/create-database-parallel-data-warehouse.md)  
  
使用一個 load 命令載入多個檔案時，所有拒絕的資料列都會寫入相同的拒絕檔案。 拒絕檔案不會顯示哪一個輸入檔包含每個拒絕的資料列。  
  
空字串不應當做分隔符號使用。 當使用空字串做為資料列分隔符號時，載入將會失敗。 當做資料行分隔符號使用時，載入會忽略分隔符號，並繼續使用預設的 "|" 做為資料行分隔符號。 當做字串分隔符號使用時，會忽略空字串，並套用預設行為。  
  
## <a name="locking-behavior"></a>鎖定行為  
**dwloader**鎖定行為會根據*load_mode_option*而有所不同。  
  
-   **附加**-附加是建議的和最常見的選項。 Append 會將資料載入至臨時表。 下面將詳細說明鎖定。  
  
-   **快速附加**-將快速附加載入至最後一個資料表，以取得 ExclusiveUpdate 表鎖，而且是唯一不使用臨時表的模式。  
  
-   **重載**-重載會將資料載入至臨時表，而且需要臨時表和最終資料表的獨佔鎖定。 不建議將重載用於並行作業。  
  
-   **upsert** -upsert 會將資料載入至臨時表，然後從臨時表執行合併作業至最後一個資料表。 Upsert 不需要最後一個資料表的獨佔鎖定。 使用 upsert 時，效能可能會有所不同。 在您的環境中測試行為。  
  
### <a name="locking-behavior"></a>鎖定行為  
**附加模式鎖定**  
  
Append 可以在多重交易模式下執行（使用-m 引數），但它不是交易安全的。 因此，應該使用 append 做為交易式作業（不使用-m 引數）。 可惜的是，在最後的插入選取作業期間，交易模式目前的速度比多重交易模式慢六倍。  
  
[附加] 模式會以兩個階段來載入資料。 第一個階段會同時將來源檔案的資料載入至臨時表（可能發生片段）。 第二階段會將資料從臨時表載入至最後一個資料表。 第二個階段會執行**INSERT INTO .。。選取 WITH （TABLOCK）** 運算。 下表顯示最後一個資料表的鎖定行為，以及使用 [附加] 模式時的記錄行為：  
  
|資料表類型|多重交易<br />模式（-m）|資料表是空的|支援的並行|記錄|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|堆積|是|是|是|有限|  
|堆積|是|否|是|有限|  
|堆積|否|是|否|有限|  
|堆積|否|否|否|有限|  
|Cl|是|是|否|有限|  
|Cl|是|否|是|完整|  
|Cl|否|是|否|有限|  
|Cl|否|否|是|完整|  
  
上表顯示使用附加模式載入至堆積或叢集索引（CI）資料表的**dwloader** ，其中包含或不含多重交易旗標，並載入至空白資料表或非空白資料表。 每個這種負載組合的鎖定和記錄行為都會顯示在資料表中。 例如，以附加模式將（第2個）階段載入至不含多重交易模式的叢集索引，且在空的資料表中，將會在資料表上建立獨佔鎖定，而且記錄是最小的。 這表示客戶將無法同時載入（第二個）階段，並同時查詢到空白資料表。 不過，使用相同的設定載入非空白資料表時，PDW 不會發出資料表的獨佔鎖定，而且可能會進行平行存取。 可惜的是，完整的記錄會使程式變慢。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-dwloader-example"></a>A. 簡單的 dwloader 範例  
下列範例只會顯示已選取必要選項的**載入**器起始。 其他選項則取自全域設定檔（ *loadparamfile .txt*）。  
  
使用 SQL Server 驗證的範例。  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
```  
  
使用 Windows 驗證的相同範例。  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -W -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -W -f /configfiles/loadparamfile.txt  
```  
  
針對原始程式檔和錯誤檔案使用引數的範例。  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>B. 將資料載入 AdventureWorks 資料表  
下列範例是批次腳本的一部分，它會將資料載入**AdventureWorksPDW2012**。  若要查看完整的腳本，請開啟**AdventureWorksPDW2012**安裝套件隨附的 aw_create .bat 檔案。 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

下列腳本程式碼片段會使用 dwloader 將資料載入至 Dbo.dimaccount 和 DimCurrency 資料表。 此腳本會使用乙太網路位址。 如果使用的是 [不允許]，伺服器會 *<appliance_name>* `-SQLCTL01`。  
  
```  
set server=10.193.63.134  
set user=<MyUser>  
set password=<MyPassword>  
  
set schema=AdventureWorksPDW2012.dbo  
set load="C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe"  
set mode=reload  
  
--Loads data into the AdventureWorksPDW2012.dbo.DimAccount table  
--Source data is stored in the file DimAccount.txt,   
--which is in the current directory.  
  
set t1=DimAccount  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%   
  
--Loads data from the DimCurrency.txt file into  
--AdventureWorksPDW2012.dbo.DimCurrency  
set t1=DimCurrency  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%  
```  
  
以下是 Dbo.dimaccount 資料表的 DDL。  
  
```  
CREATE TABLE DimAccount(  
AccountKey int NOT NULL,  
ParentAccountKey int,  
AccountCodeAlternateKey int,  
ParentAccountCodeAlternateKey int,  
AccountDescription nvarchar(50),  
AccountType nvarchar(50),  
Operator nvarchar(50),  
CustomMembers nvarchar(300),  
ValueType nvarchar(50),  
CustomMemberOptions nvarchar(200))  
with (CLUSTERED INDEX(AccountKey),  
DISTRIBUTION = REPLICATE);  
```  
  
以下是資料檔案 Dbo.dimaccount 的範例，其中包含要載入資料表 Dbo.dimaccount 中的資料。  
  
```  
--Sample of data in the DimAccount.txt load file.  
  
1||1||Balance Sheet||~||Currency|  
2|1|10|1|Assets|Assets|+||Currency|  
3|2|110|10|Current Assets|Assets|+||Currency|  
4|3|1110|110|Cash|Assets|+||Currency|  
5|3|1120|110|Receivables|Assets|+||Currency|  
6|5|1130|1120|Trade Receivables|Assets|+||Currency|  
7|5|1140|1120|Other Receivables|Assets|+||Currency|  
8|3|1150|110|Allowance for Bad Debt|Assets|+||Currency|  
9|3|1160|110|Inventory|Assets|+||Currency|  
10|9|1162|1160|Raw Materials|Assets|+||Currency|  
11|9|1164|1160|Work in Process|Assets|+||Currency|  
12|9|1166|1160|Finished Goods|Assets|+||Currency|  
13|3|1170|110|Deferred Taxes|Assets|+||Currency|  
```  
  
### <a name="c-load-data-from-the-command-line"></a>C. 從命令列載入資料  
範例 B 中的腳本可以藉由在命令列上輸入所有參數來取代，如下列範例所示。  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe -S <Control node IP> -E -M reload -e UTF16 -i .\DimAccount.txt -T AdventureWorksPDW2012.dbo.DimAccount -R DimAccount.bad -t "|" -r \r\n -U <login> -P <password>  
```  
  
命令列參數的描述：  
  
-   *C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe*是已安裝的 dwloader 位置。  
  
-   *-S*後面接著控制節點的 IP 位址。  
  
-   *-E*指定要將空字串載入為 Null。  
  
-   *-M reload*指定在插入來源資料之前截斷目的地資料表。  
  
-   *-e UTF16*表示來源檔案使用位元組由小到大字元編碼類型。  
  
-   *-i .\DimAccount.txt*指定資料位於名為 dbo.dimaccount 的檔案中，該檔案存在於目前目錄中。  
  
-   *-T AdventureWorksPDW2012：* 指定要接收資料之資料表的三部分名稱。  
  
-   *-R dbo.dimaccount。錯誤*指定無法載入的資料列將會寫入名為 dbo.dimaccount 的檔案。錯誤。  
  
-   *-t "|"* 指出輸入檔（Dbo.dimaccount）中的欄位是以管道字元分隔。  
  
-   *-r \r\n*會指定 dbo.dimaccount 中的每個資料列都以回車和換行字元做為結尾。  
  
-   *-U <login_name>-P <password> *指定具有執行負載之許可權的登入和密碼。  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
  
