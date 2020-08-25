---
title: dwloader 命令列載入器
description: dwloader 是平行資料倉儲 (PDW) 命令列工具，可將大量的資料表資料列載入現有的資料表。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 7dd0ccf960b53b3cd1b474f61c60a58ff9b0a2c6
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767047"
---
# <a name="dwloader-command-line-loader-for-parallel-data-warehouse"></a>平行處理資料倉儲的 dwloader 命令列載入器
**dwloader** 是平行資料倉儲 (PDW) 命令列工具，可將大量的資料表資料列載入現有的資料表。 載入資料列時，您可以將所有資料列加入至資料表的結尾 (*附加模式* 或 *fastappend 模式*) 、附加新的資料列，以及更新現有資料列 (*upsert 模式*) ，或是先刪除所有現有的資料列，然後再載入，然後再將所有資料列插入空白資料表 (*重載模式*) 。  
  
**載入資料的進程**  
  
1.  準備來源資料。  
  
    使用您自己的 ETL 流程來建立您要載入的來源資料。 來源資料必須格式化以符合目的地資料表的架構。 將來源資料儲存在一或多個文字檔中，然後將文本檔案複製到載入伺服器上的相同目錄中。 如需有關載入伺服器的詳細資訊，請參閱[取得和設定載入伺服器](acquire-and-configure-loading-server.md)。  
  
2.  準備載入選項。  
  
    決定您將使用的載入選項。 將載入選項儲存在設定檔中。 將配置檔案複製到載入伺服器上的本機位置。 本主題將說明 **dwloader** 設定選項。  
  
3.  準備載入失敗選項。  
  
    決定您想要 **dwloader** 如何處理無法載入的資料列。 為了執行負載， **dwloader** 會先將資料載入臨時表，然後將資料傳送至目的地資料表。 當載入器將資料載入到臨時表時，它會追蹤無法載入的資料列數目。 例如，未正確格式化的資料列將無法載入。 失敗的資料列會複製到拒絕檔案中。 依預設，除非您指定不同的拒絕閾值，否則負載會在第一次拒絕之後中止。  
  
4.  安裝 **dwloader**。  
  
    將 dwloader 安裝到載入伺服器上（如果尚未安裝）。 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  執行 **dwloader**。  
  
    使用適當的命令列選項，登入載入伺服器，然後執行可執行檔 **dwloader.exe** 。  
  
6.  確認結果。  
  
    您可以檢查失敗的資料列檔 (以-R) 指定，以查看是否有任何資料列無法載入。 如果這個檔案是空的，則會成功載入所有資料列。 **dwloader** 是交易式的，因此，如果任何步驟失敗 (除了拒絕的資料列) 之外，所有步驟都將回復為其初始狀態。  
  
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
顯示有關使用載入器的簡單說明資訊。 只有在未指定其他命令列參數時，才會顯示 [說明]。  
  
**-U** *login_name*  
具有適當許可權可執行載入的有效 SQL Server Authentication 登入。  
  
**-P** *password*  
SQL Server 驗證 *login_name*的密碼。  
  
**-W**  
使用 Windows 驗證。  (不需要 *login_name* 或 *密碼* 。 )  

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
使用參數檔 *parameter_file_name*取代命令列參數。 *parameter_file_name* 可以包含 *user_name* 和 *密碼*以外的任何命令列參數。 如果在命令列和參數檔中指定參數，命令列將會覆寫 file 參數。  
  
參數檔案包含一個參數， **-** 每行不含前置詞。  
  
範例：  
  
`rt=percentage`  
  
`rv=25`  
  
**-S** *target_appliance*  
指定將接收所載入資料的 SQL Server PDW 設備。  
  
*針對未進行的*連線， *target_appliance* 指定為 <設備名稱>-SQLCTL01。 若要設定此命名連接，請參閱 [設定未設定的網路介面卡](configure-infiniband-network-adapters.md)。  
  
若是 Ethernet 連線， *target_appliance* 是控制節點叢集的 IP 位址。  
  
如果省略，dwloader 會預設為安裝 dwloader 時所指定的值。 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name。* [ *架構*]。*table_name*  
目的地資料表的三部分名稱。  
  
**-I** *source_data_location*  
要載入的一或多個原始程式檔的位置。 每個原始程式檔都必須是文字檔或使用 gzip 壓縮的文字檔。 只有一個來源檔案可以壓縮成每個 gzip 檔案。  
  
若要格式化原始檔：  
  
-   來源檔案必須依照載入選項來格式化。  
  
-   原始程式檔中的每一行都包含一個資料表資料列的資料。 來源資料必須符合目的地資料表的架構。 資料行順序和資料類型也必須相符。 資料列中的每個欄位都代表目的地資料表中的資料行。  
  
-   依預設，欄位為可變長度，並以分隔符號分隔。 若要指定分隔符號類型，請使用 <variable_length_column_options> 命令列選項。 若要指定固定長度欄位，請使用 <fixed_width_column_options> 命令列選項。  
  
若要指定來源資料位置：  
  
-   來源資料位置可以是網路路徑或載入伺服器上目錄的本機路徑。  
  
-   若要指定目錄中的所有檔案，請輸入後面接著 * 萬用字元的目錄路徑。  載入器不會從來源資料位置中的任何子目錄載入檔案。 當 gzip 檔案中有目錄存在時，載入器發生錯誤。  
  
-   若要指定目錄中的某些檔案，請使用字元與 * 萬用字元的組合。  
  
若要使用一個命令載入多個檔案：  
  
-   所有檔案都必須存在於相同的目錄中。  
  
-   這些檔案必須全部是文字檔、所有 gzip 檔案，或是 text 和 gzip 檔案的組合。  
  
-   沒有任何檔案可以包含標頭資訊。  
  
-   所有檔案都必須使用相同的字元編碼類型。 請參閱-e 選項。  
  
-   所有檔案都必須載入至相同的資料表。  
  
-   所有檔案都將串連並載入，就好像它們是一個檔案一樣，而拒絕的資料列將會移至單一拒絕檔。  
  
範例：  
  
-   -i \\ \loadserver\loads\daily \\ *. gz  
  
-   -i \\ \loadserver\loads\daily \\ * .txt  
  
-   -i \\ \loadserver\loads\daily\monday. *  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\ \loadserver\loads\daily\\*  
  
**-R** *load_failure_file_name*  
如果發生載入失敗， **dwloader** 會儲存無法載入的資料列，而失敗會將失敗的資訊描述在名為 *load_failure_file_name*的檔案中。 如果此檔案已經存在，dwloader 會覆寫現有的檔案。 發生第一次失敗時，會建立*load_failure_file_name* 。 如果所有資料列都載入成功，則不會建立 *load_failure_file_name* 。  
  
**-fh** *number_header_rows*  
在 *source_data_file_name*開始時，) 要忽略 (資料列的行數。 預設值是 0。  
  
<variable_length_column_options>  
具有字元分隔可變長度資料行之 *source_data_file_name* 的選項。 依預設， *source_data_file_name* 包含可變長度資料行中的 ASCII 字元。  
  
若是 ASCII 檔案，則會將分隔符號連續放置，以表示 Null。 例如，在以管線分隔的檔案中 ( "|") ，Null 會以 "| |" 表示。 在以逗號分隔的檔案中，Null 會以 "，，" 表示。 此外，必須指定 **-E** (--emptyStringAsNull) 選項。 如需-E 的詳細資訊，請參閱下文。  
  
**-e** *character_encoding*  
指定要從資料檔案載入之資料的字元編碼類型。 選項為 ASCII (預設) 、UTF8、UTF16 或 UTF16BE，其中 UTF16 的位元組由小到大，UTF16BE 是位元組由大到小。 這些選項不區分大小寫。  
  
**-t** *field_delimiter*  
每個欄位的分隔符號 (資料列中的資料行) 。 欄位分隔符號是其中一或多個 ASCII escape 字元或 ASCII 十六進位值。  
  
|Name|逸出字元|十六進位字元|  
|--------|--------------------|-----------------|  
|索引標籤|\t|0x09|  
|回車 (CR) |\r|0x0d|  
|換行字元 (LF) |\n|0x0a|  
|CRLF|\r\n|0x0d0x0a|  
|Comma (逗號)|','|0x2c|  
|雙引號|\\"|0x22|  
|單引號|\\'|0x27|  
  
若要在命令列上指定管道字元，請用雙引號括住 "|"。 這會避免命令列剖析器進行解釋。 其他字元則以單引號括住。  
  
範例：  
  
-t "|"  
  
-t ' '  
  
-t 0x0a  
  
-t \t  
  
-t ' ~ | ~ '  
  
**-r** *row_delimiter*  
源資料檔案中每個資料列的分隔符號。 資料列分隔符號是一或多個 ASCII 值。  
  
若要指定換行字元 (CR) 、換行 (LF) 或定位字元作為分隔符號，您可以使用 escape 字元 ( \r、\n、\t) 或其十六進位值 (0x、0d、09) 。 若要將任何其他特殊字元指定為分隔符號，請使用其十六進位值。  
  
CR + LF 的範例：  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR 的範例：  
  
-r \r  
  
-r 0x0d  
  
LF 範例：  
  
-r \n  
  
-r 0x0a  
  
Unix 需要 LF。 Windows 需要 CR。  
  
**-s** *string_delimiter*  
文字分隔輸入檔的字串資料類型欄位分隔符號。 字串分隔符號是一或多個 ASCII 值。  您可以將它指定為字元 (例如，-s * ) 或十六進位值 (例如雙引號) 的-s 0x22。  
  
範例：  
  
！  
  
-s 0x22  
  
< fixed_width_column_options>  
具有固定長度資料行之源資料檔案的選項。 依預設， *source_data_file_name* 包含可變長度資料行中的 ASCII 字元。  
  
當-e 是 UTF8 時，不支援固定寬度資料行。  
  
**-w** *fixed_width_config_file*  
設定檔案的路徑和名稱，指定每個資料行中的字元數。 必須指定每個欄位。  
  
這個檔案必須位於載入伺服器上。 路徑可以是 UNC、相對路徑或絕對路徑。 *Fixed_width_config_file*中的每一行都包含一個資料行的名稱，以及該資料行的字元數。 每個資料行都有一行，如下所示，檔案中的順序必須符合目的地資料表中的順序：  
  
*column_name* =*num_chars*  
  
*column_name* =*num_chars*  
  
固定寬度設定檔範例：  
  
SalesCode = 3  
  
SalesID = 10  
  
*Source_data_file_name*中的範例行：  
  
230Shirts0056  
  
320Towels1356  
  
在上述範例中，第一個載入的資料列會有 SalesCode = ' 230 ' 和 SalesID = ' Shirts0056 '。 第二個載入的資料列會有 SalesCode = ' 320 ' 和 SaleID = ' Towels1356 '。  
  
如需如何在固定寬度模式中處理開頭和尾端空格或資料類型轉換的詳細資訊，請參閱 [dwloader 的資料類型轉換規則](dwloader-data-type-conversion-rules.md)。  
  
**-e** *character_encoding*  
指定要從資料檔案載入之資料的字元編碼類型。 選項為 ASCII (預設) 、UTF8、UTF16 或 UTF16BE，其中 UTF16 的位元組由小到大，UTF16BE 是位元組由大到小。 這些選項不區分大小寫。  
  
當-e 是 UTF8 時，不支援固定寬度資料行。  
  
**-r** *row_delimiter*  
源資料檔案中每個資料列的分隔符號。 資料列分隔符號是一或多個 ASCII 值。  
  
若要指定換行字元 (CR) 、換行 (LF) 或定位字元作為分隔符號，您可以使用 escape 字元 ( \r、\n、\t) 或其十六進位值 (0x、0d、09) 。 若要將任何其他特殊字元指定為分隔符號，請使用其十六進位值。  
  
CR + LF 的範例：  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR 的範例：  
  
-r \r  
  
-r 0x0d  
  
LF 範例：  
  
-r \n  
  
-r 0x0a  
  
Unix 需要 LF。 Windows 需要 CR。  
  
**-D** { **ymd** \| ydm \| mdy \| myd \| dmy \| dym \| *custom_date_format* }  
針對輸入檔中的所有日期時間欄位，指定每月 (m) 、day (d) 和 year (y) 。 預設順序為 ymd。 若要為相同的原始程式檔指定多個順序格式，請使用-dt 選項。  
  
ymd \| dmy  
ydm 和 dmy 允許相同的輸入格式。 兩者都允許年份在日期的開頭或結尾。 例如，針對 **ydm** 和 **dmy** 日期格式，輸入檔中可能會有2013-02-03 或02-03-2013。  
  
ydm  
您只能將格式化為 ydm 的輸入載入資料類型 datetime 和 Smalldatetime 資料行中。 您無法將 ydm 值載入 datetime2、date 或 datetimeoffset 資料類型的資料行。  
  
mdy  
mdy 允許 \<month> \<space> \<day> \<comma> \<year> 。  
  
1975年1月1日的 mdy 輸入資料範例：  
  
-   1975年1月1日  
  
-   Jan 01，75  
  
-   Jan/1/75  
  
-   01011975  
  
myd  
2010年3月4日的輸入檔範例：03-2010-04、3/2010/4  
  
dym  
2010年3月4日的輸入檔範例：04-2010-03、4/2010/3  
  
*custom_date_format*  
*custom_date_format* 是自訂日期格式 (例如，MM/dd/yyyy) ，且僅供回溯相容性之用。 dwloader 不會強制使用自訂日期格式。 相反地，當您指定自訂日期格式時， **dwloader** 會將它轉換成相對應的 ymd、ydm、mdy、myd、dym 或 dmy 設定。  
  
例如，如果您指定-D MM/dd/yyyy，dwloader 預期所有的日期輸入會以 month、day 和 year 來排序， (mdy) 。 它不會強制使用自訂日期格式所指定的2個字元數、2位數的天數和4位數年份。 以下是日期格式為-D MM/dd/yyyy：01/02/2013、Jan. 02.2013、1/2/2013 時，可在輸入檔中格式化日期的一些方式範例  
  
如需更完整的格式設定資訊，請參閱 [dwloader 的資料類型轉換規則](dwloader-data-type-conversion-rules.md)。  
  
**-dt** *datetime_format_file*  
每個日期時間格式都是在名為 *datetime_format_file*的檔案中指定。 不同于命令列參數，包含空格的檔案參數不得以雙引號括住。 當您載入資料時，不能改變日期時間格式。 來源資料檔及其在目的地資料表中的對應資料行必須具有相同的格式。  
  
每一行都包含目的地資料表中的資料行名稱和其日期時間格式。  
  
範例：  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
將包含臨時表的資料庫名稱。 預設值是使用-T 選項指定的資料庫，也就是目的地資料表的資料庫。 如需有關使用臨時資料庫的詳細資訊，請參閱 [建立臨時資料庫](staging-database.md)。  
  
**-M** *load_mode_option*  
指定是否要附加、upsert 或重載資料。 預設模式為 [附加]。  
  
附加  
載入器會將資料列插入目的地資料表中現有資料列的結尾。  
  
fastappend  
載入器會直接將資料列插入目的地資料表中現有資料列的結尾，而不使用臨時表。 fastappend 需要多重交易 (-m) 選項。 使用 fastappend 時，不能指定暫存資料庫。 不會使用 fastappend 復原，這表示從失敗或中止的負載復原必須由您自己的負載處理常式來處理。  
  
upsert **-K**  *merge_column* [,.。。*n* ]  
載入器會使用 SQL Server Merge 語句來更新現有的資料列，並插入新的資料列。  
  
-K 選項會指定要做為合併依據的資料行。 這些資料行會形成合併索引鍵，這應該代表唯一的資料列。 如果合併索引鍵存在於目的地資料表中，則會更新該資料列。 如果合併索引鍵不存在於目的地資料表中，則會附加資料列。  
  
若為雜湊分散式資料表，合併索引鍵必須是或包含散發資料行。  
  
針對複寫資料表，合併索引鍵是一或多個資料行的組合。 這些資料行是根據應用程式的需求來指定。  
  
多個資料行必須以逗號分隔，而且不能有空格，或以空格分隔並以單引號括住。  
  
如果來源資料表中有兩個數據列具有相符的合併索引鍵值，其各自的資料列必須相同。  
  
重新 載入  
載入器會在插入來源資料之前截斷目的地資料表。  
  
**-b** *batchsize*  
建議僅供 Microsoft 支援服務使用， *batchsize* 是 DMS 在計算節點上 SQL Server 實例中執行之大量複製的 SQL Server 批次大小。  當指定 *batchsize* 時，SQL Server PDW 將會覆寫針對每個負載動態計算的批次載入大小。  
  
從 SQL Server 2012 PDW 開始，控制節點預設會動態計算每個負載的批次大小。 這項自動計算是根據數個參數，例如記憶體大小、目標資料表類型、目標資料表架構、載入類型、檔案大小，以及使用者的資源類別。  
  
例如，如果載入模式是 FASTAPPEND，且資料表有叢集資料行存放區索引，SQL Server PDW 預設會嘗試使用1048576的批次大小，如此資料列群組就會變成封閉並直接載入資料行存放區，而不會經過差異存放區。 如果記憶體不允許批次大小為1048576，dwloader 會選擇較小的 batchsize。  
  
如果載入類型是 FASTAPPEND， *batchsize* 就會套用至將資料載入資料表中，否則 *batchsize* 會套用至將資料載入至臨時表。  
  
<reject_options>  
指定選項，以決定載入器將允許的載入失敗數目。 如果載入失敗超過閾值，載入器將會停止，而且不會認可任何資料列。  
  
**-rt** { **value** | 百分比}  
指定- **rv** *reject_value*選項中的-*reject_value*是否為常值的資料列數目 (值) 或失敗率 (百分比) 。 預設值為 [值]。  
  
百分比選項是根據-rs 選項的間隔時間所發生的即時計算。  
  
例如，如果載入器嘗試載入100個數據列，而25個失敗且75成功，則失敗率為25%。  
  
**-rv** *reject_value*  
指定在停止載入之前，允許的資料列拒絕的數目或百分比。 **-Rt**選項可決定*reject_value*是指資料列的數目或資料列的百分比。  
  
預設 *reject_value* 為0。  
  
搭配-rt 值使用時，當拒絕的資料列計數超過 reject_value 時，載入器會停止負載。  
  
使用 with-rt 百分比時，載入器會計算間隔 (-rs 選項) 的百分比。 因此，失敗的資料列百分比可能會超過 *reject_value*。  
  
**-rs** *reject_sample_size*  
與選項搭配使用， `-rt percentage` 以指定增量百分比檢查。 例如，如果 reject_sample_size 為1000，則載入器會在嘗試載入1000資料列之後，計算失敗的資料列百分比。 它會在嘗試載入每個額外的1000資料列之後，重新計算失敗的資料列百分比。  
  
**-c**  
移除 char、Nchar、Varchar 和 Nvarchar 欄位左邊和右邊的空白字元。 將只包含空白字元的每個欄位轉換為空字串。  
  
範例：  
  
' ' 被截斷為 ' '  
  
' abc ' 會被截斷為 ' abc '  
  
當搭配-E 使用-c 時，會先發生-E 作業。 只包含空白字元的欄位會轉換成空字串，而不是 Null。  
  
**-E**  
將空字串轉換為 Null。 預設值是不要執行這些轉換。  
  
**-m**  
在載入的第二個階段使用多重交易模式;將資料從臨時表載入至分散式資料表時。  
  
若使用 **-m**，SQL Server PDW 會以平行方式執行和認可載入。 執行的速度比預設載入模式快許多，但不是交易安全的。  
  
如果沒有 **-m**，SQL Server PDW 會在每個計算節點內的散發中，以及在計算節點之間，以序列方式來執行和認可負載。 這個方法比多重交易模式慢，但是是交易安全的。  
  
**-m** 是選擇性的，可供 *附加*、 *重載*及 *upsert*。  
  
fastappend 需要 **-m** 。  
  
**-m** 不能與複寫的資料表搭配使用。  
  
**-m** 只適用于第二個載入階段。 它不適用於第一個載入階段;將資料載入至臨時表。  
  
沒有具有多重交易模式的復原，這表示從失敗或中止的負載復原必須由您自己的負載處理常式來處理。  
  
建議您只在載入空白資料表時使用 **-m** ，如此您就可以在不遺失資料的情況下復原。 若要從載入失敗復原：卸載目的地資料表、解決載入問題、重新建立目的地資料表，然後再次執行載入。  
  
**-N**  
確認目標設備具有來自受信任授權單位的有效 SQL Server PDW 憑證。 使用此方法可協助確保您的資料不會被攻擊者攔截，並傳送到未授權的位置。 憑證必須已安裝在設備上。 安裝憑證的唯一支援方式是讓裝置管理員使用 Configuration Manager 工具進行安裝。 如果您不確定設備是否已安裝受信任的憑證，請詢問您的設備系統管理員。  
  
**-se**  
略過載入空白檔案。 這也會略過解壓縮空的 gzip 檔案。

**-l**  
適用于 CU 7.4 更新，指定可載入的最大資料列長度 (位元組) 。 有效的值為介於32768到33554432之間的整數。 只有在需要時才使用載入大型資料列 (大於 32KB) ，因為這樣會在用戶端和伺服器上配置更多記憶體。
  
## <a name="return-code-values"></a>傳回碼值  
0 (成功) 或其他整數值 (失敗)   
  
在命令視窗或批次檔中，使用 `errorlevel` 顯示傳回碼。 例如：  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
使用 PowerShell 時，請使用 `$LastExitCode` 。  
  
## <a name="permissions"></a>權限  
需要載入許可權和適用的許可權 (在目的地資料表上插入、更新、刪除) 。 需要 CREATE 許可權 (，才能在暫存資料庫上) 建立臨時表。 如果未使用暫存資料庫，則需要在目的地資料庫上建立許可權。 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>一般備註  
如需使用 dwloader 載入時資料類型轉換的詳細資訊，請參閱 [dwloader 的資料類型轉換規則](dwloader-data-type-conversion-rules.md)。  
  
如果參數包含一或多個空格，請用雙引號括住參數。  
  
您應該從其安裝位置執行載入器。 Dwloader 可執行檔會隨設備預先安裝，且位於 C:\Program Files\Microsoft SQL Server Data Warehouse\DWLoader 目錄中。  
  
您可以藉由指定參數檔中指定的參數做為命令列參數，來覆寫參數檔中指定的參數 (-f 選項) 。  
  
您可以同時執行多個載入器的實例。 載入器實例的最大數目是預先設定的，而且無法變更。 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
載入的資料在設備上可能需要更多或更少的空間，而不是來源位置。 您可以使用資料子集來執行測試匯入，以預估磁片耗用量。  
  
雖然 **dwloader** 是交易程式，並會在失敗時正常回復，但一旦大量載入順利完成，就無法回復。 若要取消使用中的 **dwloader** 處理常式，請輸入 CTRL + C。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
同時發生之所有載入的總大小必須小於資料庫的 LOG_SIZE，而我們建議所有並行載入的總大小小於 LOG_SIZE 的50%。 若要達到這種大小的限制，您可以將大型載入分割成多個批次。 如需 LOG_SIZE 的詳細資訊，請參閱[建立資料庫](../t-sql/statements/create-database-transact-sql.md?view=aps-pdw-2016)。  
  
載入多個具有一個 load 命令的檔案時，所有拒絕的資料列都會寫入相同的拒絕檔案中。 拒絕檔案不會顯示每個被拒絕的資料列包含哪個輸入檔。  
  
空字串不應用作為分隔符號。 當使用空字串做為資料列分隔符號時，載入將會失敗。 當做資料行分隔符號使用時，載入會忽略分隔符號，並繼續使用預設的 "|" 作為資料行分隔符號。 當做字串分隔符號使用時，會忽略空字串並套用預設行為。  
  
## <a name="locking-behavior"></a>鎖定行為  
**dwloader** 鎖定行為會視 *load_mode_option*而有所不同。  
  
-   [**附加**-附加] 是建議的選項，也是最常見的選項。 附加會將資料載入至臨時表。 以下將詳細說明鎖定。  
  
-   **快速附加** -快速附加-將直接附加到最後的資料表（ExclusiveUpdate 表鎖定），而且是唯一不使用臨時表的模式。  
  
-   **重載** -重載會將資料載入臨時表，而且需要臨時表和最終資料表的獨佔鎖定。 不建議針對並行作業使用重載。  
  
-   **upsert** -upsert 會將資料載入至臨時表，然後執行從臨時表到最後資料表的合併作業。 Upsert 不需要最終資料表的獨佔鎖定。 使用 upsert 時，效能可能會有所不同。 在您的環境中測試行為。  
  
### <a name="locking-behavior"></a>鎖定行為  
**附加模式鎖定**  
  
您可以使用-m) 引數，在多交易式模式中執行 Append (，但它並不是交易安全的。 因此，「附加」應該當做交易式作業使用， (不需使用-m 引數) 。 可惜的是，在最後一次插入選取作業期間，交易模式目前大約比多重交易模式慢6倍。  
  
附加模式會以兩個階段載入資料。 第一個階段會將資料從來源檔案載入至臨時表， (片段會) 發生。 第二階段將資料從臨時表載入至最終資料表。 第二個階段會執行 **INSERT INTO .。。SELECT WITH (TABLOCK) ** 作業。 下表顯示最終資料表上的鎖定行為，以及使用附加模式時的記錄行為：  
  
|資料表類型|多重交易<br />模式 (-m) |資料表是空的|支援平行存取|記錄|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|堆積|是|是|是|基本|  
|堆積|是|否|是|基本|  
|堆積|否|是|否|基本|  
|堆積|否|否|否|基本|  
|Cl|是|是|否|基本|  
|Cl|是|否|是|完整|  
|Cl|否|是|否|基本|  
|Cl|否|否|是|完整|  
  
上表顯示 **dwloader** 使用附加模式載入至堆積或叢集索引 (CI) 資料表（包含或不含多重交易旗標），以及載入空白資料表或非空白資料表中。 每個這類載入的鎖定和記錄行為都會顯示在資料表中。 比方說，在沒有多重交易模式的情況下，將具有附加模式的 (第 2) 階段載入至叢集索引，會讓 PDW 在資料表上建立獨佔鎖定，而且記錄是最基本的。 這表示，客戶將無法在第2個) 階段載入 (，並同時查詢到空白資料表。 但是，將相同的設定載入至非空白資料表時，PDW 不會在資料表上發出獨佔鎖定，而且可能會有平行存取。 可惜的是，會進行完整記錄，使進程變慢。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-dwloader-example"></a>A. 簡單 dwloader 範例  
下列範例只會顯示已選取所需選項的 **載入** 器起始。 其他選項取自全域設定檔案， *loadparamfile.txt*。  
  
使用 SQL Server Authentication 的範例。  
  
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
  
### <a name="b-load-data-into-an-adventureworks-table"></a>B. 將資料載入至 AdventureWorks 資料表  
下列範例是批次腳本的一部分，可將資料載入 **AdventureWorksPDW2012**中。  若要查看完整的腳本，請開啟 **AdventureWorksPDW2012** 安裝套件隨附的 aw_create.bat 檔案。 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

下列腳本程式碼片段會使用 dwloader 將資料載入至 DimAccount 和 DimCurrency 資料表。 此腳本會使用乙太網路位址。 如果使用的是 [自動]，則會 *<伺服器 appliance_name>* `-SQLCTL01` 。  
  
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
  
以下是 DimAccount 資料表的 DDL。  
  
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
  
以下是資料檔案的範例，DimAccount.txt，其中包含要載入至資料表 DimAccount 的資料。  
  
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
您可以在命令列上輸入所有參數來取代範例 B 中的腳本，如下列範例所示。  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe -S <Control node IP> -E -M reload -e UTF16 -i .\DimAccount.txt -T AdventureWorksPDW2012.dbo.DimAccount -R DimAccount.bad -t "|" -r \r\n -U <login> -P <password>  
```  
  
命令列參數的描述：  
  
-   *C:\Program Files\Microsoft SQL Server 平行資料 Warehouse\100\dwloader.exe* 是 dwloader.exe 的安裝位置。  
  
-   *-S* 後面接著控制節點的 IP 位址。  
  
-   *-E* 指定將空字串載入為 Null。  
  
-   *-M 重載* 指定在插入來源資料之前截斷目的地資料表。  
  
-   *-e UTF16* 表示來源檔案使用位元組由小到小的字元編碼類型。  
  
-   *-i .\DimAccount.txt* 指定資料位於目前目錄中名為 DimAccount.txt 的檔案。  
  
-   *-T AdventureWorksPDW2012. DimAccount* 指定要接收資料之資料表的3部分名稱。  
  
-   *-R DimAccount。不正確* 的指定無法載入的資料列將會寫入名為 DimAccount 的檔案中。不正確。  
  
-   *-t "|"* 表示輸入檔中的欄位（DimAccount.txt）會以管道字元分隔。  
  
-   *-r \r\n* 指定 DimAccount.txt 中的每個資料列都會以換行字元和換行字元作為結尾。  
  
-   *-U <login_name>-P <password> *指定具有執行載入許可權之登入的登入和密碼。  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
