---
title: dwloader 命令列載入器-Parallel Data Warehouse |Microsoft Docs
description: dwloader 是 Parallel Data Warehouse (PDW) 的命令列工具，將資料表的資料列大量載入至現有的資料表。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: df30a9b849b987b5514a1824f25736a82587da09
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66175042"
---
# <a name="dwloader-command-line-loader-for-parallel-data-warehouse"></a>dwloader 平行處理資料倉儲的命令列載入器
**dwloader**是 Parallel Data Warehouse (PDW) 的命令列工具，將資料表的資料列大量載入至現有的資料表。 載入時的資料列，您可以將所有資料列加入資料表的結尾 (*附加模式*或是*fastappend 模式*)、 附加新資料列，並更新現有的資料列 (*upsert 模式*)，或刪除所有現有之前載入的資料列，然後再將所有資料列插入空的資料表 (*重新載入模式*)。  
  
**載入資料的程序**  
  
1.  準備來源資料。  
  
    您可以使用自己的 ETL 程序來建立您想要載入的來源資料。 來源資料必須格式化為目的地資料表的結構描述相符。 將來源資料儲存至一或多個文字檔案，並將文字檔複製到相同的目錄載入伺服器上。 載入伺服器的相關資訊，請參閱[取得並設定載入伺服器](acquire-and-configure-loading-server.md)  
  
2.  準備載入選項。  
  
    決定您將使用哪一個載入選項。 在組態檔中儲存的載入選項。 將組態檔複製到載入伺服器上的本機位置。 **Dwloader**組態選項本主題中所述。  
  
3.  準備載入失敗的選項。  
  
    決定您要如何**dwloader**來處理無法載入的資料列。 若要執行載入， **dwloader**第一次將資料載入暫存資料表，然後將資料傳送至目的地資料表。 載入器會將資料載入暫存資料表，因為它會追蹤無法載入的資料列數目。 例如，格式不正確的資料列將無法載入。 失敗的資料列會複製到拒絕檔案。 根據預設，負載會中止後的第一個拒絕除非您指定不同的拒絕臨界值。  
  
4.  安裝**dwloader**。  
  
    如果尚未安裝，請安裝 dwloader 載入伺服器上。 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  執行**dwloader**。  
  
    載入伺服器登入，並執行可執行檔**dwloader.exe**以適當的命令列選項。  
  
6.  驗證結果。  
  
    您可以檢查失敗要請參閱是否無法載入任何資料列的資料列 （使用-R 指定） 的檔案。 如果此檔案是空的所有資料列成功載入。 **dwloader**是交易式，所以如果任何步驟失敗 （而非拒絕的資料列） 時，所有的步驟將會回復為其初始狀態。  
  
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
顯示有關使用載入器的簡單說明資訊。 如果未不指定任何其他命令列參數，只會顯示說明。  
  
**-U** *login_name*  
具有適當的權限來執行載入的有效 SQL Server 驗證登入。  
  
**-P** *password*  
SQL Server 驗證密碼*login_name*。  
  
**-W**  
使用 Windows 驗證。 (沒有*login_name*或是*密碼*必要。) 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
使用參數檔案， *parameter_file_name*，來取代命令列參數。 *parameter_file_name*可以包含任何命令列參數，除了*user_name*並*密碼*。 如果在命令列和參數檔案中指定的參數，命令列覆寫檔案參數。  
  
參數檔案包含一個參數，不含 **-** 前置詞，每一行。  
  
範例:  
  
`rt=percentage`  
  
`rv=25`  
  
* *-S***target_appliance*  
指定會接收載入的資料的 SQL Server PDW 應用裝置。  
  
*Infiniband 連線*， *target_appliance*指定為 < 設備名稱 >-SQLCTL01。 若要設定該已命名的連線，請參閱[設定的 InfiniBand 網路介面卡](configure-infiniband-network-adapters.md)。  
  
為乙太網路連線*target_appliance*控制節點的叢集 IP 位址。  
  
如果省略，dwloader 預設 dwloader 已安裝時所指定的值。 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name.* [*schema*].*table_name*  
在目的地資料表的三部分名稱。  
  
* *-I***source_data_location*  
若要載入的一或多個來源檔案的位置。 每個原始程式檔必須是文字檔或以 gzip 壓縮的文字檔。 只有一個來源檔案可以壓縮到每個 gzip 檔案。  
  
若要格式化的原始程式檔：  
  
-   原始程式檔的格式必須根據的載入選項。  
  
-   原始程式檔中的每一行都包含一個資料表資料列的資料。 來源資料必須符合目的地資料表結構的描述。 此外，也必須符合資料行順序和資料類型。 每個資料列中的欄位表示目的地資料表中的資料行。  
  
-   根據預設，具有變動長度的欄位，和以分隔符號分隔。 若要指定的分隔符號類型，請使用 < variable_length_column_options > 命令列選項。 若要指定固定的長度欄位，請使用 < fixed_width_column_options > 命令列選項。  
  
若要指定來源資料的位置：  
  
-   來源資料的位置可以是網路路徑或本機路徑來載入伺服器上的目錄。  
  
-   若要指定所有檔案的目錄中，輸入目錄路徑，後面加上 * 萬用字元。  載入器未載入從來源資料的位置中的任何子目錄中的檔案。 載入器時的錯誤的目錄存在於 gzip 檔案。  
  
-   若要指定某些檔案的目錄中，使用字元的組合和 * 萬用字元。  
  
若要載入多個檔案，以一個命令：  
  
-   所有檔案必須都存在於相同的目錄。  
  
-   檔案必須是所有的文字檔案、 所有 gzip 檔案或文字和 gzip 檔案的組合。  
  
-   沒有任何檔案可以包含標頭資訊。  
  
-   所有檔案都必須都使用相同的字元編碼類型。 請參閱-e 選項。  
  
-   所有檔案必須都載入到相同資料表中。  
  
-   即將串連並載入就好像它們是一個檔案，並拒絕的資料列會移至單一的拒絕檔案的所有檔案。  
  
範例:  
  
-   -i \\\loadserver\loads\daily\\*.gz  
  
-   -i \\\loadserver\loads\daily\\*.txt  
  
-   -i \\\loadserver\loads\daily\monday.*  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\\loadserver\loads\daily\\*  
  
**-R** *load_failure_file_name*  
如果發生載入失敗**dwloader**會儲存無法載入和失敗描述失敗的資訊，在名為的資料列*load_failure_file_name*。 如果此檔案已經存在，dwloader 會覆寫現有的檔案。 *load_failure_file_name*第一次失敗發生時建立。 如果成功，載入所有資料列*load_failure_file_name*就不會建立。  
  
**-fh** *number_header_rows*  
若要忽略開頭的行 （列） 數目*source_data_file_name*。 預設值是 0。  
  
<variable_length_column_options>  
選項*source_data_file_name*具有字元分隔可變長度資料行。 根據預設， *source_data_file_name*包含可變長度資料行中的 ASCII 字元。  
  
對於 ASCII 檔案，Null 會以連續放置分隔符號。 例如，在直立線符號分隔的檔案 ("|")，null 值會以"| |"。 在以逗號分隔的檔案，以表示 NULL"、"。 此外， **-E** (-emptyStringAsNull) 必須指定選項。 如需詳細資訊，在-E，如下所示。  
  
**-e** *character_encoding*  
指定資料要載入資料檔中的字元編碼類型。 選項為 ASCII （預設值）、 UTF8、 UTF16 或 UTF16BE，其中 UTF16 是稍微位元組由小到大而 UTF16BE 是 big endian。 這些選項是不區分大小寫。  
  
**-t** *field_delimiter*  
每個欄位 （資料行） 中的資料列分隔符號。 欄位分隔符號是一或多個這些 ASCII 逸出字元或 ASCII 十六進位值。  
  
|名稱|逸出字元|十六進位字元|  
|--------|--------------------|-----------------|  
|索引標籤|\t|0x09|  
|歸位字元 (CR)|\r|0x0d|  
|換行字元 (LF)|\n|0x0a|  
|CRLF|\r\n|0x0d0x0a|  
|逗點|','|0x2c|  
|雙引號|\\"|0x22|  
|單引號|\\'|0x27|  
  
若要在命令列上指定直立線符號字元，將它括在雙引號括住，"|"。 這可避免錯誤解譯命令列剖析器。 其他字元會以單引號括住。  
  
範例:  
  
-t "|"  
  
-t ' '  
  
-t 0x0a  
  
-t \t  
  
-t '~|~'  
  
**-r** *row_delimiter*  
來源資料檔案的每一個資料列分隔符號。 資料列分隔符號是一或多個 ASCII 值。  
  
若要指定做為分隔符號的歸位字元 (CR)、 換行字元 (LF) 或 tab 字元，您可以使用逸出字元 （\r、 \n、 \t） 或 0 x （0d，09），其十六進位值。 若要指定其他任何特殊字元做為分隔符號，請使用其十六進位值。  
  
CR LF + 的範例：  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR 的範例：  
  
-r \r  
  
-r 0x0d  
  
LF 的範例：  
  
-r \n  
  
-r 0x0a  
  
需要 Unix LF。 需要 Windows CR。  
  
**-s** *string_delimiter*  
字串資料的分隔符號類型的文字分隔的輸入檔案的欄位。 字串分隔符號是一或多個 ASCII 值。  它可以指定為字元 (例如 s *) 或十六進位值 (例如，-s 0x22 雙引號)。  
  
範例:  
  
-s *  
  
-s 0x22  
  
< fixed_width_column_options>  
具有固定長度資料行的來源資料檔案的選項。 根據預設， *source_data_file_name*包含可變長度資料行中的 ASCII 字元。  
  
UTF8-e 時不支援固定的寬度資料行。  
  
**-w** *fixed_width_config_file*  
路徑和名稱的組態檔，在每個資料行中指定的字元數。 必須指定每個欄位。  
  
這個檔案必須位於載入伺服器。 路徑可以是 UNC、 相對或絕對路徑。 中的每一行*fixed_width_config_file*包含該資料行的一個資料行和字元數的名稱。 有一列，每個資料行，如下所示，並在檔案中的順序必須符合目的地資料表中的順序：  
  
*column_name*=*num_chars*  
  
*column_name*=*num_chars*  
  
固定寬度的組態檔的範例：  
  
SalesCode=3  
  
SalesID=10  
  
行中的範例*source_data_file_name*:  
  
230Shirts0056  
  
320Towels1356  
  
在上述範例中，第一個載入的資料列必須 SalesCode = '230' 和 SalesID = 'Shirts0056'。 第二個載入的資料列會有 SalesCode = '320' 和 SaleID = 'Towels1356'。  
  
如需如何處理開頭和尾端空格或資料類型轉換，以固定的寬度模式的資訊，請參閱[資料類型轉換規則 dwloader](dwloader-data-type-conversion-rules.md)。  
  
**-e** *character_encoding*  
指定資料要載入資料檔中的字元編碼類型。 選項為 ASCII （預設值）、 UTF8、 UTF16 或 UTF16BE，其中 UTF16 是稍微位元組由小到大而 UTF16BE 是 big endian。 這些選項是不區分大小寫。  
  
UTF8-e 時不支援固定的寬度資料行。  
  
**-r** *row_delimiter*  
來源資料檔案的每一個資料列分隔符號。 資料列分隔符號是一或多個 ASCII 值。  
  
若要指定做為分隔符號的歸位字元 (CR)、 換行字元 (LF) 或 tab 字元，您可以使用逸出字元 （\r、 \n、 \t） 或 0 x （0d，09），其十六進位值。 若要指定其他任何特殊字元做為分隔符號，請使用其十六進位值。  
  
CR LF + 的範例：  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR 的範例：  
  
-r \r  
  
-r 0x0d  
  
LF 的範例：  
  
-r \n  
  
-r 0x0a  
  
需要 Unix LF。 需要 Windows CR。  
  
**-D** { **ymd** | ydm | mdy | myd |  dmy | dym | *custom_date_format* }  
在輸入檔中指定的月份 (m)、 一天 (d) 和年份 (y) 的所有日期時間欄位的順序。 預設順序是 ymd。 若要指定多個相同的原始程式檔的順序格式，請使用-dt 選項。  
  
ymd |dmy  
ydm 和 dmy 可讓相同的輸入的格式。 同時允許要在開頭或結束日期的年份。 例如，兩個**ydm**並**dmy**日期格式，您無法在輸入檔中有 2013年-02-03 或 02-03-2013年。  
  
ydm  
您只能載入輸入格式為 ydm，插入的資料型別 datetime 和 smalldatetime 的資料行。 無法載入 ydm 值設定為 datetime2、 日期或 datetimeoffset 資料類型的資料行。  
  
mdy  
可讓 mdy <month> <space> <day> <comma> <year>。  
  
1975 年 1 月 1 日的 mdy 輸入資料的範例：  
  
-   1975 年 1 月 1日日  
  
-   75 Jan 01，  
  
-   Jan/1/75  
  
-   01011975  
  
myd  
年 3 月的輸入檔範例 04,2010:03-2010-04, 3/2010/4  
  
dym  
2010 年 3 月 04 日的輸入的檔範例：04-2010-03, 4/2010/3  
  
*custom_date_format*  
*custom_date_format*是自訂的日期格式 (例如，MM/dd/yyyy)，而且包含基於回溯相容性。 dwloader 不會強制使用的自訂日期格式。 相反地，當您指定自訂日期格式**dwloader**會將它轉換成 ymd、 ydm、 mdy、 myd、 dym，或 dmy 對應的設定。  
  
例如，如果您指定-D MM/dd/yyyy，dwloader 預期所有輸入第一，排序使用月份的日期則日，然後年 (mdy)。 它不會強制執行 2 個字元的幾個月、 2 位數的天數和所指定的自訂日期格式的 4 位數年份。 以下是一些範例舉出-D MM/dd/yyyy 的日期格式時，可以在輸入檔中設定日期：01/02/2013，Jan.02.2013，2013 年 1 月 2 日  
  
更廣泛的格式資訊，請參閱[資料類型轉換規則 dwloader](dwloader-data-type-conversion-rules.md)。  
  
**-dt** *datetime_format_file*  
名為的檔案中指定每個日期時間格式*datetime_format_file*。 不同於命令列參數，包含空格的檔案參數不必須括在雙引號。 當您載入資料，您無法改變的日期時間格式。 來源資料檔案和目的地資料表中的對應資料行必須具有相同的格式。  
  
每一行都包含在目的地資料表，而且它的日期時間格式的資料行的名稱。  
  
範例:  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
將包含暫存資料表的資料庫名稱。 預設為使用-T 選項時，也就是目的地資料表的資料庫所指定的資料庫。 如需使用暫存資料庫的詳細資訊，請參閱[建立暫存資料庫](staging-database.md)。  
  
**-M** *load_mode_option*  
指定是否要附加 upsert，或重新載入資料。 預設模式是附加。  
  
附加  
載入器會插入資料列結尾的目的地資料表中的現有資料列。  
  
fastappend  
載入器而不需使用暫存資料表時，目的地資料表中的現有資料列的結尾，請以直接插入資料列。 fastappend 需要多的交易 (-m) 選項。 使用 fastappend 時，就無法指定暫存資料庫。 與 fastappend，這表示從失敗或已中止負載復原必須由您自己的載入程序沒有回復。  
  
upsert **-K**  *merge_column* [ ,...*n* ]  
載入器會使用 SQL Server Merge 陳述式來更新現有的資料列，並插入新資料列。  
  
-K 選項指定為基礎的合併的資料行。 這些資料行形成合併索引鍵，應該代表唯一的資料列。 如果合併索引鍵存在於目的地資料表中，會更新資料列。 如果合併索引鍵不存在於目的地資料表，則會附加資料列。  
  
雜湊分散式資料表，必須是合併索引鍵，或將其包含散發資料行中。  
  
對於複寫的資料表，合併索引鍵會是一或多個資料行組合。 根據應用程式的需求會指定這些資料行。  
  
多個資料行必須與不含空格，以逗號分隔或逗號分隔的空格且以單引號括住。  
  
如果來源資料表中的兩個資料列有相符的合併索引鍵值，其各自的資料列必須相同。  
  
重新載入  
載入器會截斷目的地資料表之前它會插入的來源資料。  
  
**-b** *batchsize*  
依照 Microsoft 支援服務，建議僅供使用*batchsize*是大量複製到計算節點上的 SQL Server 執行個體的 DMS 執行的 SQL Server 批次大小。  當*batchsize*指定，則 SQL Server PDW 會覆寫每個負載會動態計算的批次載入大小。  
  
從 SQL Server 2012 PDW，控制節點以動態方式計算每次載入的批次大小預設值。 這項自動計算取決於數個參數，例如記憶體大小、 目標資料表類型，目標資料表結構描述、 載入類型、 檔案大小和使用者的資源類別。  
  
比方說，如果負載模式是 FASTAPPEND 資料表具有叢集資料行存放區索引，SQL Server PDW 會依預設會嘗試使用 1,048,576 的批次大小，以便將會關閉資料列群組，並直接載入到資料行存放區而不會通過差異存放區。 如果記憶體不允許 1,048,576 的批次大小，dwloader 選擇較小的 batchsize。  
  
如果負載類型是 FASTAPPEND， *batchsize*適用於將資料載入資料表，否則為*batchsize*適用於將資料載入暫存資料表。  
  
<reject_options>  
指定決定，則載入器可讓載入失敗數目的選項。 如果載入失敗超過閾值時，載入器將會中止，並認可任何資料列。  
  
**-rt** { **value** | percentage }  
指定是否-*reject_value*中 **-rv** *reject_value*選項是常值的數字的資料列 （值） 或失敗 （百分比） 的速率。 預設為值。  
  
[百分比] 選項是即時計算所根據的 rs 選項的間隔發生。  
  
例如，如果載入器嘗試載入 100 個資料列和 25 失敗，75 成功，然後失敗率為 25%。  
  
**-rv** *reject_value*  
指定數目或百分比的資料列拒絕暫停負載之前，先允許。 **-Rt**選項會決定如果*reject_value*是指資料列數目或百分比的資料列。  
  
預設值*reject_value*為 0。  
  
-Rt 值搭配使用時，載入器已拒絕的資料列計數超過 reject_value 時，就會停止負載。  
  
當使用以-rt 百分比，則載入器會不時計算百分比 (-rs 選項)。 因此，失敗的資料列百分比可能會超過*reject_value*。  
  
**-rs** *reject_sample_size*  
搭配`-rt percentage`選項來指定增量百分比檢查。 比方說，如果 reject_sample_size 1000，則載入器會計算失敗資料列的百分比已嘗試載入 1000 個資料列之後。 它會重新計算失敗資料列的百分比之後它會嘗試載入每個額外的 1000 個資料列。  
  
**-c**  
從左側與右側 char、 nchar、 varchar 和 nvarchar 欄位中移除泛空白字元。 將轉換每個欄位，只包含泛空白字元的字元為空字串。  
  
範例:  
  
'' 取得截斷為 '  
  
'abc' 取得截斷成 'abc'  
  
時使用-E，使用-c-E 的作業，就會發生第一次。 只包含空格字元的欄位都會轉換為空字串，而不是 NULL。  
  
**-E**  
將空字串轉換為 NULL。 預設值將不會執行這些轉換。  
  
**-m**  
用於載入，第二個階段的多重交易模式當資料從暫存表格載入分散式資料表。  
  
具有 **-m**，SQL Server PDW 執行並認可以平行方式載入。 這比預設的載入模式，更快速執行，但不是交易安全。  
  
不含 **-m**，SQL Server PDW 執行，並依序認可的負載，散發內每個計算節點，且同時的計算節點之間。 這個方法會低於多的交易模式，而是交易安全。  
  
**-m**是選擇性*附加*，*重新載入*，和*upsert*。  
  
**-m** fastappend 需要。  
  
**-m**不適用於複寫資料表。  
  
**-m**只適用於第二個 「 載入 」 階段。 不適用於在第一次載入階段載入暫存資料表中的資料。  
  
沒有任何復原多的交易模式中，這表示從失敗或已中止負載復原必須由您自己的載入程序。  
  
我們建議您使用 **-m**載入空白資料表，以便您可以復原不會遺失資料時，才。 若要從負載失敗中復原： 卸除目的地資料表，解決負載問題，重新建立目的地資料表，然後再次執行負載。  
  
**-N**  
確認目標應用裝置具有有效的 SQL Server PDW 憑證來自受信任的授權單位。 使用它來協助確保您的資料未由攻擊者攔截，並傳送給未經授權的位置。 在應用裝置上時，必須已安裝憑證。 支援的唯一方法，將憑證安裝為應用裝置系統管理員使用組態管理員工具進行安裝。 如果您不確定應用裝置是否受信任的憑證安裝要求您的應用裝置系統管理員。  
  
**-se**  
略過載入空白檔案。 這也會略過正在解壓縮空 gzip 檔案。

**-l**  
可用 CU7.4 更新中，指定可載入的最大資料列長度 （以位元組為單位）。 有效值為 32768 到 33554432 之間的整數。 只使用需要時載入大型資料列 （超過 32 KB），因為這將會配置更多的記憶體，在用戶端和伺服器上。
  
## <a name="return-code-values"></a>傳回碼值  
0 （成功） 或其他的整數值 （失敗）  
  
在命令視窗或批次檔中，使用`errorlevel`来顯示的傳回碼。 例如：  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
使用 PowerShell 時，使用`$LastExitCode`。  
  
## <a name="permissions"></a>Permissions  
需要載入權限和適用的權限 (INSERT、 UPDATE、 DELETE) 的目的地資料表。 需要暫存資料庫的 CREATE 權限 （用於建立暫存資料表）。 如果未使用暫存資料庫，在目的地資料庫上需要建立權限。 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>一般備註  
如需資料類型轉換時使用 dwloader 載入資訊，請參閱[資料類型轉換規則 dwloader](dwloader-data-type-conversion-rules.md)。  
  
如果參數包含一個或多個空格，括住雙引號括住的參數。  
  
您應該執行載入器，從安裝位置。 可執行檔 dwloader 預先安裝應用裝置，並會位於 C:\Program Files\Microsoft SQL Server 資料 Warehouse\DWLoader 目錄中。  
  
您可以覆寫參數檔中指定的參數 (-f 選項) 將它指定為命令列參數。  
  
您可以同時執行多個執行個體的載入器。 載入器執行個體數目上限預先設定的無法變更。 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
載入的資料可能需要較多或較少的空間比應用裝置中的來源位置上。 您可以執行測試匯入的估計磁碟耗用量資料的子集。  
  
雖然**dwloader**是交易的程序且會回復依正常程序失敗，無法回復已順利完成大量載入之後上, 一步。 若要取消作用**dwloader**程序時，輸入 CTRL + C。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
必須小於資料庫的 LOG_SIZE，建議您所有的並行載入的總大小同時發生的所有載入的總大小是小於 50%的 LOG_SIZE。 若要達到這個大小限制，您可以將大量載入分割成多個批次。 如需有關 LOG_SIZE 的詳細資訊，請參閱[CREATE DATABASE](../t-sql/statements/create-database-parallel-data-warehouse.md)  
  
載入時使用一種負載命令的多個檔案，所有已拒絕的資料列會寫入相同的拒絕檔案。 拒絕檔案不會顯示哪一個輸入的檔包含每個已拒絕的資料列。  
  
空字串不應做為分隔符號。 當空字串做為資料列分隔符號時，載入將會失敗。 當做資料行分隔符號使用時，負載會忽略分隔符號，並會繼續使用預設值"|"做為資料行分隔符號。 當做字串分隔符號使用時，會忽略空的字串，並套用預設行為。  
  
## <a name="locking-behavior"></a>鎖定行為  
**dwloader**鎖定行為有所不同*load_mode_option*。  
  
-   **附加**-附加時的建議與最常見的選項。 附加資料載入至暫存資料表。 以下將詳細說明的鎖定。  
  
-   **快速附加**-快速附加直接載入最終資料表採用 ExclusiveUpdate 資料表鎖定，而且不會使用暫存資料表的唯一模式。  
  
-   **重新載入**-重新載入將資料載入至暫存資料表，而且需要暫存資料表和最終的資料表的獨佔鎖定。 並行作業不被建議重新載入。  
  
-   **upsert** -Upsert 將資料載入至暫存資料表中，而再執行合併作業從暫存表格最終的資料表。 更新插入不需要最後一個資料表的獨佔鎖定。 使用插入時，效能可能會有所不同。 在您的環境中測試的行為。  
  
### <a name="locking-behavior"></a>鎖定行為  
**附加模式的鎖定**  
  
附加可以在 （使用-m 引數） 的多個交易式模式執行，但是不安全的交易。 因此附加應該做為交易式作業 （不使用-m 引數）。 不幸的是，最終插入選取作業期間，交易式模式低於目前六倍多的交易式模式。  
  
Append 模式在兩個階段中載入資料。 第一個階段將資料從原始程式檔載入暫存資料表同時 （分散可能會發生）。 第二階段會將資料從暫存資料表載入到最終的資料表。 第二個階段執行**INSERT INTO...選取 WITH (TABLOCK)** 作業。 下表顯示最終的資料表，鎖定行為，並使用時的記錄行為附加模式：  
  
|資料表類型|多重交易<br />模式 (-m)|資料表是空的|支援的並行存取|記錄|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|堆積|是|是|是|最小|  
|堆積|是|否|是|最小|  
|堆積|否|是|否|最小|  
|堆積|否|否|否|最小|  
|cl|是|是|否|最小|  
|cl|是|否|是|完整|  
|cl|否|是|否|最小|  
|cl|否|否|是|完整|  
  
以上表所示**dwloader**使用附加模式載入堆積或叢集的索引 (CI) 資料表，包含或不含多個交易式的旗標，並載入空白資料表或非空白資料表。 鎖定和記錄行為的負載的每個這類的組合，會顯示在資料表中。 比方說，載入 (第 2) 的階段，以附加模式，而不需要多個交易式模式的叢集索引和至空白資料表會有在資料表上建立獨佔鎖定的 PDW 和記錄是最小。 這表示，客戶將無法將 （第 2 個） 的階段和查詢同時載入空白資料表。 不過，PDW 時載入到非空白資料表相同的組態，不會發出之資料表的獨佔鎖定，並行有可能。 不幸的是，完整記錄發生時，降低程序。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-dwloader-example"></a>A. Dwloader 的簡單範例  
下列範例顯示的起始**載入器**只有選取的必要選項。 其他選項會全域組態檔中，從*loadparamfile.txt*。  
  
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
  
使用引數的原始程式檔和錯誤檔案的範例。  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>B. 資料載入至 AdventureWorks 的資料表  
下列範例是將資料載入的批次指令碼的一部分**AdventureWorksPDW2012**。  若要檢視完整的指令碼，請開啟 aw_create.bat 檔案隨附**AdventureWorksPDW2012**安裝套件。 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

下列指令碼程式碼片段會使用 dwloader 載入到 DimAccount 和 DimCurrency 資料表的資料。 此指令碼會使用乙太網路位址。 如果它使用 InfiniBand，伺服器會 *< appliance_name >* `-SQLCTL01`。  
  
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
  
以下是資料檔案，而 DimAccount.txt，包含要載入 DimAccount 的資料表之資料的範例。  
  
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
範例 B 中的指令碼可以取代藉由在命令列中，輸入所有參數，如下列範例所示。  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe -S <Control node IP> -E -M reload -e UTF16 -i .\DimAccount.txt -T AdventureWorksPDW2012.dbo.DimAccount -R DimAccount.bad -t "|" -r \r\n -U <login> -P <password>  
```  
  
命令列參數的描述：  
  
-   *C:\Program Files\Microsoft SQL Server 平行資料 Warehouse\100\dwloader.exe* dwloader.exe 的安裝位置。  
  
-   *-S*後面跟著 [控制] 節點的 IP 位址。  
  
-   *-E*指定要載入空字串為 NULL。  
  
-   *-M 重新載入*指定截斷目的地資料表之前它會插入的來源資料。  
  
-   *-e UTF16*指出原始程式檔使用的小小的位元組由小到大字元編碼類型。  
  
-   *-i.\DimAccount.txt*指定的資料位於名為 DimAccount.txt 存在於目前的目錄中的檔案。  
  
-   *-T AdventureWorksPDW2012.dbo.DimAccount*指定要接收資料之資料表的 3 段式名稱。  
  
-   *-R DimAccount.bad*指定無法載入的資料列會寫入名為 DimAccount.bad 的檔案。  
  
-   *-t"|"* 指出輸入檔，也就是 DimAccount.txt 中的欄位會以縱線字元分隔。  
  
-   *-r \r\n*指定 DimAccount.txt 每個資料列結尾歸位字元和換行字元。  
  
-   *-U < >-P login_name <password>* 指定的登入和密碼登入具有權限來執行載入。  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
  
