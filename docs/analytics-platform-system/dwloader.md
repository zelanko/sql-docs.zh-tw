---
title: "dwloader 平行處理資料倉儲的命令列載入器"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "* * dwloader * * 是 Parallel Data Warehouse (PDW) 的命令列工具，可將資料表資料列中大量載入現有的資料表。"
ms.date: 11/04/2016
ms.topic: article
ms.assetid: f79b8354-fca5-41f7-81da-031fc2570a7c
caps.latest.revision: "90"
ms.openlocfilehash: 0335005e2e0590efe28a0cbf7dff6aaacfea331f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="dwloader-command-line-loader"></a>dwloader 命令列載入器
**dwloader** Parallel Data Warehouse (PDW) 的命令列工具，可將資料表資料列中大量載入現有的資料表。 當載入的資料列，您可以將所有資料列加入到資料表結尾 (*附加模式*或*fastappend 模式*)、 附加新資料列，並更新現有的資料列 (*upsert 模式*)，或刪除所有現有之前載入的資料列，然後再將所有資料列插入空的資料表 (*重新載入模式*)。  
  
**用於載入資料的程序**  
  
1.  準備來源資料。  
  
    使用您自己的 ETL 程序，以建立您想要載入的來源資料。 來源資料必須格式化為符合目的地資料表的結構描述。 來源資料儲存到一個或多個文字檔案，並將文字檔案複製到您載入的伺服器上相同的目錄。 載入伺服器的相關資訊，請參閱[取得和設定載入伺服器](acquire-and-configure-loading-server.md)  
  
2.  準備載入選項。  
  
    決定您將使用哪一個載入選項。 儲存在組態檔中的載入選項。 將組態檔複製到您載入伺服器上的本機位置。 **Dwloader**本主題會描述組態選項。  
  
3.  準備載入失敗選項。  
  
    決定您要如何**dwloader**來處理無法載入的資料列。 若要執行載入， **dwloader**第一次將資料載入暫存資料表，然後將資料傳送至目的地資料表。 載入器會將資料載入暫存資料表，因為它會追蹤無法載入的資料列數目。 例如，將無法載入格式不正確的資料列。 失敗的資料列會複製到拒絕檔案。 根據預設，負載中止後第一個拒絕除非您指定不同的拒絕臨界值。  
  
4.  安裝**dwloader**。  
  
    如果尚未安裝，請安裝 dwloader 到載入伺服器。 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  執行**dwloader**。  
  
    登入來載入伺服器並執行可執行檔**dwloader.exe**以適當的命令列選項。  
  
6.  驗證結果。  
  
    您可以檢查失敗要請參閱是否無法載入任何資料列的資料列 （使用-R 指定） 的檔案。 這個檔案是空的如果成功載入的所有資料列。 **dwloader**為交易式，所以如果任何步驟失敗 （而不被拒絕的資料列），所有的步驟將會回復為其初始狀態。  
  
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
}  
```  
  
## <a name="arguments"></a>引數  
**-h**  
顯示關於使用載入器的簡單說明資訊。 如果未不指定任何其他命令列參數，只會顯示說明。  
  
**-U** *login_name*  
具有適當的權限來執行載入的有效 SQL Server 驗證登入。  
  
**-P** *password*  
SQL Server 驗證密碼*login_name*。  
  
**-W**  
使用 Windows 驗證。 (無*login_name*或*密碼*需要。) 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
使用參數檔案， *parameter_file_name*，來取代命令列參數。 *parameter_file_name*可以包含任何命令列參數，除了*user_name*和*密碼*。 如果在命令列上和參數檔案中，將指定的參數，命令列覆寫檔案參數。  
  
參數檔案包含一個參數，而不 **-** 前置詞，每行。  
  
範例:  
  
`rt=percentage`  
  
`rv=25`  
  
**-S***target_appliance*  
指定 SQL Server PDW 應用裝置，將會收到所載入的資料。  
  
*Infiniband 連接*， *target_appliance*指定為 < 應用裝置名稱 >-SQLCTL01。 若要設定具名連接，請參閱[設定 InfiniBand 網路介面卡](configure-infiniband-network-adapters.md)。  
  
為乙太網路連線*target_appliance*控制節點的叢集 IP 位址。  
  
如果省略，dwloader 預設 dwloader 安裝時所指定的值。 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name。*[*結構描述*]。*table_name*  
在目的地資料表的三部分名稱。  
  
**-I***source_data_location*  
要載入的一個或多個來源檔案的位置。 每個原始程式檔必須是文字檔案或以 gzip 壓縮的文字檔。 只有一個原始程式檔可以壓縮成每個 gzip 檔案中。  
  
若要格式化的原始程式檔：  
  
-   原始程式檔必須格式化根據載入選項。  
  
-   原始程式檔中的每一行都包含一個資料表資料列的資料。 來源資料必須符合目的地資料表的結構描述。 也必須符合資料行順序和資料類型。 每個資料列中的欄位代表的目的地資料表中的資料行。  
  
-   根據預設，欄位是可變長度，並以分隔符號分隔。 若要指定的分隔符號類型，使用 < variable_length_column_options > 命令列選項。 若要指定固定的長度欄位，請使用 < fixed_width_column_options > 命令列選項。  
  
若要指定來源資料的位置：  
  
-   來源資料的位置可以是網路路徑或本機路徑上載入伺服器的目錄。  
  
-   若要指定所有檔案的目錄中，輸入目錄路徑，後面接著 * 萬用字元。  載入器不會載入從來源資料的位置中的任何子目錄的檔案... 當目錄存在於 gzip 檔載入器錯誤。  
  
-   若要指定部分檔案的目錄中，使用 字元的組合和 * 萬用字元。  
  
若要載入一個命令具有多個檔案：  
  
-   所有檔案必須都存在於相同的目錄。  
  
-   所有文字檔案、 所有的 gzip 檔或結合文字和 gzip 檔，必須是檔案。  
  
-   沒有任何檔案可以包含標頭資訊。  
  
-   所有檔案必須都使用相同的字元編碼類型。 請參閱-e 選項。  
  
-   所有檔案必須都載入到相同資料表中。  
  
-   即將串連並載入，就好像它們是一個檔案，和已拒絕的資料列將會移至單一拒絕檔案的所有檔案。  
  
範例:  
  
-   -i \\\loadserver\loads\daily\\*.gz  
  
-   -i \\\loadserver\loads\daily\\*.txt  
  
-   -i \\\loadserver\loads\daily\monday.*  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\\loadserver\loads\daily\\*  
  
**-R** *load_failure_file_name*  
如果沒有載入失敗**dwloader**儲存無法載入及失敗描述檔案中的失敗資訊的資料列*load_failure_file_name*。 如果這個檔案已經存在，dwloader 會覆寫現有的檔案。 *load_failure_file_name*第一次失敗時建立。 如果所有資料列載入成功， *load_failure_file_name*就不會建立。  
  
**-fh** *number_header_rows*  
若要忽略開頭的行 （列） 數目*source_data_file_name*。 預設值是 0。  
  
< variable_length_column_options >  
選項*source_data_file_name*具有字元分隔可變長度資料行。 根據預設， *source_data_file_name*包含可變長度資料行中的 ASCII 字元。  
  
對於 ASCII 檔案，會由左至右連續放置分隔符號來表示 Null。 管線分隔檔案中，例如 ("|")，null 值會以"| |"。 在以逗號分隔的檔案，以表示 NULL"、"。 此外， **-E** (-emptyStringAsNull) 必須指定選項。 如需詳細資訊，在-E，請參閱下文。  
  
**-e** *character_encoding*  
指定資料要從資料檔載入的字元編碼類型。 選項為 ASCII （預設值）、 UTF8、 UTF16 或 UTF16BE UTF16 是由小到大而且 UTF16BE big endian。 這些選項是不區分大小寫。  
  
**-t** *field_delimiter*  
每個欄位 （資料行） 中的資料列分隔符號。 欄位分隔符號是一或多個這些 ASCII 逸出字元或 ASCII 十六進位值...  
  
|名稱|逸出字元|十六進位字元|  
|--------|--------------------|-----------------|  
|索引標籤|\t|0x09|  
|歸位字元 (CR)|\r|0x0d|  
|換行字元 (LF)|\n|0x0a|  
|CRLF|\r\n|0x0d0x0a|  
|逗點|','|0x2c|  
|雙引號|\\"|0x22|  
|單引號|\\'|0x27|  
  
若要在命令列上指定縱線字元，將它括在雙引號中，"|"。 這樣可避免錯誤解譯命令列剖析器。 其他字元會以單引號括住。  
  
範例:  
  
-t"|"  
  
-t ' '  
  
-t 0x0a  
  
-t \t  
  
-t ' ~ | ~'  
  
**-r** *row_delimiter*  
來源資料檔的每一個資料列分隔符號。 資料列分隔符號是一或多個 ASCII 值。  
  
若要指定做為分隔符號的歸位字元 (CR)、 換行字元 (LF) 或 tab 字元，您可以使用逸出字元 （\r、 \n、 \t） 或 0 x （0d 09） 其十六進位值。 若要指定做為分隔符號的任何其他特殊字元，使用其十六進位值。  
  
CR LF + 的範例包括：  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR 的範例包括：  
  
-r \r  
  
-r 0x0d  
  
LF 的範例包括：  
  
-r \n  
  
-r 0x0a  
  
需要 unix LF。 需要 Windows CR。  
  
**-s** *string_delimiter*  
字串資料的分隔符號類型的文字分隔的輸入檔的欄位。 字串分隔符號是一或多個 ASCII 值。  它可以指定為字元 (例如，-s *) 或十六進位值 (例如，-s 0x22 的雙引號括住)。  
  
範例:  
  
-s *  
  
-s 0x22  
  
< fixed_width_column_options >  
具有固定長度資料行的來源資料檔案的選項。 根據預設， *source_data_file_name*包含可變長度資料行中的 ASCII 字元。  
  
UTF8 – e 時不支援固定的寬度資料行。  
  
**-w** *fixed_width_config_file*  
路徑和名稱的組態檔，每個資料行中指定的字元數。 必須指定每個欄位。  
  
這個檔案必須位於上載入伺服器。 路徑可以是 UNC、 相對或絕對路徑。 中的每一行*fixed_width_config_file*包含該資料行的一個資料行和字元數的名稱。 資料行，每一行，如下所示，而檔案中的順序必須符合目的地資料表中的順序：  
  
*column_name*=*num_chars*  
  
*column_name*=*num_chars*  
  
固定寬度的組態檔的範例：  
  
SalesCode = 3  
  
SalesID = 10  
  
範例程式碼行中*source_data_file_name*:  
  
230Shirts0056  
  
320Towels1356  
  
在上述範例中，第一個載入的資料列會有 SalesCode = '230' 以及 SalesID = 'Shirts0056'。 第二個載入的資料列會有 SalesCode = '320' 和 SaleID = 'Towels1356'。  
  
如需如何處理開頭和尾端空格或資料類型轉換，以固定的寬度模式資訊，請參閱[資料類型轉換規則 dwloader](dwloader-data-type-conversion-rules.md)。  
  
**-e** *character_encoding*  
指定資料要從資料檔載入的字元編碼類型。 選項為 ASCII （預設值）、 UTF8、 UTF16 或 UTF16BE UTF16 是由小到大而且 UTF16BE big endian。 這些選項是不區分大小寫。  
  
UTF8 – e 時不支援固定的寬度資料行。  
  
**-r** *row_delimiter*  
來源資料檔的每一個資料列分隔符號。 資料列分隔符號是一或多個 ASCII 值。  
  
若要指定做為分隔符號的歸位字元 (CR)、 換行字元 (LF) 或 tab 字元，您可以使用逸出字元 （\r、 \n、 \t） 或 0 x （0d 09） 其十六進位值。 若要指定做為分隔符號的任何其他特殊字元，使用其十六進位值。  
  
CR LF + 的範例包括：  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR 的範例包括：  
  
-r \r  
  
-r 0x0d  
  
LF 的範例包括：  
  
-r \n  
  
-r 0x0a  
  
需要 unix LF。 需要 Windows CR。  
  
**-D** { **ymd** | ydm | mdy | myd | dmy |dym |*custom_date_format* }  
在輸入檔中指定的月份 (m)、 (d) 的日期和年份 (y) 的所有日期時間欄位的順序。 預設順序是 ymd。 若要指定多個相同的原始程式檔的順序格式，請使用-dt 選項。  
  
ymd |dmy  
ydm 和 dmy 可讓相同的輸入的格式。 允許在開頭或結束日期的年份。 例如，兩個**ydm**和**dmy**日期格式，您無法在 2013年-02-03 或 02-03-2013 輸入檔。  
  
ydm  
您只能載入輸入格式為 ydm，插入的資料型別 datetime 和 smalldatetime 資料行。 無法載入 ydm 值設定為 datetime2、 日期或 datetimeoffset 資料類型的資料行。  
  
mdy  
可讓 mdy <month> <space> <day> <comma> <year>。  
  
1975 年 1 月 1 日的 mdy 輸入資料的範例包括：  
  
-   1975 年 1 月 1日日  
  
-   75 年 1 月 01 日  
  
-   Jan/1/75  
  
-   01011975  
  
myd  
年 3 月的輸入檔範例 04,2010: 03-2010年-04、 4/3/2010年  
  
dym  
2010 年 3 月 04 的輸入檔範例： 04-2010年-03，3/4/2010年  
  
*custom_date_format*  
*custom_date_format*是自訂的日期格式 (例如，MM/dd/yyyy)，而且包含回溯相容性。 dwloader 不 enfoce 自訂日期格式。 相反地，當您指定自訂的日期格式， **dwloader**會將它轉換成對應的 ymd、 ydm、 mdy、 myd、 dym 或 dmy 的設定。  
  
例如，如果您指定 – D MM/dd/yyyy，dwloader 預期所有輸入都以月份第一次，排序的日期則日期，然後年份 (mdy)。 它不會強制執行 2 2 位數天和 4 位數年份的自訂日期格式所指定的字元個月。 以下是一些範例的日期格式 – D MM/dd/yyyy 時，可以在輸入檔中設定日期的方式： 01/02/2013，Jan.02.2013，2013 年 1 月 2 日  
  
更廣泛的格式設定資訊，請參閱[資料類型轉換規則 dwloader](dwloader-data-type-conversion-rules.md)。  
  
**-dt** *datetime_format_file*  
名為的檔案中指定每個日期時間格式*datetime_format_file*。 不同於命令列參數，包含空格的檔案參數不必須用雙引號括住。 當您載入資料，您無法改變日期時間格式。 來源資料檔和其對應的資料行與目的地資料表必須具有相同的格式。  
  
每一行都包含在目的地資料表和其日期時間格式的資料行的名稱。  
  
範例:  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
將包含暫存資料表的資料庫名稱。 預設值是使用-T 選項，這是目的地資料表的資料庫指定的資料庫。 如需使用暫存資料庫的詳細資訊，請參閱[建立暫存資料庫](staging-database.md)。  
  
**-M** *load_mode_option*  
指定是否要將附加，請更新插入，或重新載入資料。 預設模式是附加。  
  
附加  
載入器會將資料列插入目的地資料表中的現有資料列的結尾。  
  
fastappend  
載入器插入資料列直接管理，而不需要使用暫存資料表時，目的地資料表中的現有資料列的結尾。 fastappend 需要多重交易 (– m) 選項。 使用 fastappend 時無法指定暫存資料庫。 沒有任何與 fastappend，這表示您自己的載入處理序必須處理從失敗或已中止載入復原的復原。  
  
upsert **-K***merge_column* [，...*n* ]    
載入器會使用 SQL Server Merge 陳述式來更新現有的資料列，並插入新資料列。  
  
-K 選項指定要合併的基礎資料行的資料行。 這些資料行形成應該代表唯一的資料列的合併索引鍵。 如果合併索引鍵存在於目的地資料表時，會更新資料列。 如果合併索引鍵不存在於目的地資料表，則會附加資料列。  
  
雜湊散發的資料表，必須是合併索引鍵，或將其包含散發資料行中。  
  
對於複寫的資料表，合併索引鍵會是一個或多個資料行的組合。 根據應用程式的需求會指定這些資料行。  
  
多個資料行必須不含空格，以逗號分隔或逗號分隔，以空格且以單引號括住。  
  
如果來源資料表中的兩個資料列有相符的合併值，其各自的資料列必須相同。  
  
重新載入  
載入器會截斷目的地資料表，才能將來源資料。  
  
**-b** *batchsize*  
建議您只有使用 Microsoft 支援*batchsize*是大量複製的 DMS 執行到計算節點上的 SQL Server 執行個體的 SQL Server 批次大小。  當*batchsize*指定，則 SQL Server PDW 將會覆寫每個載入的動態計算的批次載入大小。  
  
從 SQL Server 2012 PDW，控制節點以動態方式計算每個載入的批次大小預設。 這項自動計算根據數個參數，例如記憶體大小、 目標資料表類型，目標資料表結構描述、 負載類型、 檔案大小和使用者的資源類別。  
  
比方說，如果則 FASTAPPEND 載入模式，且資料表具有叢集資料行存放區索引，SQL Server PDW 會依預設會嘗試使用 1,048,576 的批次大小，以便將會關閉資料列群組和直接載入至資料行存放區而不需要透過差異存放區。 如果記憶體，不允許 1,048,576 的批次大小，dwloader 選擇較小的 batchsize。  
  
如果負載類型是 FASTAPPEND， *batchsize*適用於將資料載入資料表，否則*batchsize*適用於將資料載入暫存資料表。  
  
< reject_options >  
指定選項來判斷允許載入器載入失敗的數目。 如果載入失敗超過閾值時，載入器將會中止，並認可的任何資料列。  
  
**-rt** {**值**| 百分比}  
指定是否-*reject_value*中**-rv** *reject_value*選項是常值的數字的資料列 （值） 或失敗 （百分比） 的速率。 預設為值。  
  
百分比選項是即時計算所發生在根據 cd-r 選項的時間間隔。  
  
例如，如果失敗，則載入器會嘗試載入 100 個資料列和 25 75 成功，然後失敗率為 25%。  
  
**-rv** *reject_value*  
指定數目或百分比的資料列之拒絕停止負載之前，先允許。 **-Rt**選項會決定如果*reject_value*指的資料列數目或百分比的資料列。  
  
預設值*reject_value*為 0。  
  
-Rt 值搭配使用時，載入器已拒絕的資料列計數超過 reject_value 時，就會停止負載。  
  
當使用-rt 百分比，載入器會計算百分比的間隔 (-rs 選項)。 因此，失敗的資料列百分比可能會超過*reject_value*。  
  
**cd-r** *reject_sample_size*  
搭配`-rt percentage`選項以指定的增量百分比檢查。 例如，如果 reject_sample_size 1000，載入器會計算失敗資料列的百分比之後已嘗試載入 1000 個資料列。 它會重新計算失敗資料列的百分比，它會嘗試載入每個額外的 1000 個資料列之後。  
  
**-c**  
從左邊和右邊 char、 nchar、 varchar 和 nvarchar 欄位移除空白字元。 將每個欄位，只包含空白字元的字元為空字串轉換。  
  
範例:  
  
'' 取得截斷成 '  
  
'abc' 取得截斷成 'abc'  
  
使用-E，使用 – c 時 – E 作業先發生。 只包含空格字元的欄位都會轉換為空字串，而不是 NULL。  
  
**-E**  
空字串轉換為 NULL。 預設為不執行這些轉換。  
  
**-m**  
多重交易模式用於載入; 第二個階段當資料從暫存表格載入分散式的資料表。  
  
與**– m**，SQL Server PDW 執行並認可以平行方式載入。 這會執行速度，比預設值載入模式，但不是交易安全。  
  
不含**– m**，SQL Server PDW 執行並載入以序列方式認可跨分佈在每個計算節點中，同時在計算節點之間。 這個方法會低於多重交易模式，但為交易安全。  
  
**-m**是選擇性的*附加*，*重新載入*，和*upsert*。  
  
**-m** fastappend 需要。  
  
**-m**不適用於複寫的資料表。  
  
**-m**只適用於第二個 「 載入 」 階段。 它不會套用到第一個載入階段;將資料載入至暫存資料表。  
  
沒有任何多重交易模式中，這表示您自己的載入處理序必須處理從失敗或已中止負載復原的復原。  
  
我們建議您使用**– m**才載入空白資料表，以便您可以復原不會遺失資料。 若要從負載失敗中復原： 卸除目的地資料表、 解決負載問題，重新建立目的地資料表，然後再次執行負載。  
  
**-N**  
確認目標裝置具有有效的 SQL Server PDW 憑證來自受信任的授權單位。 使用它來協助確保您的資料不會遭到攻擊者攔截並傳送給未經授權的位置。 應用裝置上必須已安裝憑證。 若要安裝憑證的唯一支援的方法是應用裝置系統管理員所要使用組態管理員工具進行安裝。 如果您不確定應用裝置是否有安裝受信任的憑證要求您的應用裝置系統管理員。  
  
**-se**  
略過載入空白檔案。 這也會略過解壓縮空 gzip 檔案。  
  
## <a name="return-code-values"></a>傳回碼值  
0 （成功） 或其他整數值 （失敗）  
  
在命令視窗或批次檔中，使用`errorlevel`来顯示的傳回碼。 例如：  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
使用 PowerShell 時，使用`$LastExitCode`。  
  
## <a name="permissions"></a>Permissions  
需要負載權限，以及目的地資料表上有可用的權限 (INSERT、 UPDATE、 DELETE)。 需要的暫存資料庫空間 （適用於建立的暫存資料表） 的建立權限。 如果未使用暫存資料庫，在目的地資料庫上需要建立權限。 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>一般備註  
Dwloader 與載入時，資料類型轉換詳細資訊，請參閱[資料類型轉換規則 dwloader](dwloader-data-type-conversion-rules.md)。  
  
如果參數包含一個或多個空格，就用雙引號括住參數。  
  
您應該執行載入器，從安裝位置。 可執行檔 dwloader 與設備已預先安裝，並會位於 C:\Program Files\Microsoft SQL Server 資料 Warehouse\DWLoader 目錄中。  
  
您可以覆寫參數檔案中指定的參數 (-f 選項) 將它指定為命令列參數。  
  
您可以同時執行多個執行個體載入器。 載入器執行個體數目上限預先設定的無法變更。 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
載入的資料可能需要更多或更少的空間比應用裝置中的來源位置上。 您可以執行測試匯入的資料來預估磁碟耗用量的子集。  
  
雖然**dwloader**是交易的程序並將回復依正常程序失敗，無法回復已順利完成大量載入之後，傳回。 若要取消作用中**dwloader**處理中，輸入 CTRL + C。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
必須小於 LOG_SIZE 資料庫，而且建議所有的並行負載的大小總計同時發生的所有載入的總大小為小於 50%LOG_SIZE。 若要達到這個大小限制，您可以將大量載入分割成多個批次。 如需有關 LOG_SIZE 的詳細資訊，請參閱[建立資料庫](../t-sql/statements/create-database-parallel-data-warehouse.md)  
  
載入時使用一種負載命令的多個檔案，拒絕的所有資料列會寫入相同的 「 拒絕 」 檔案。 拒絕檔案不會顯示哪一個輸入的檔包含每個已拒絕的資料列。  
  
空字串不應做為分隔符號。 使用空字串時，做為資料列分隔符號，載入將會失敗。 當做資料行分隔符號使用時，載入會忽略分隔符號，並繼續使用預設的"|"做為資料行分隔符號。 當做字串分隔符號使用時，會忽略空的字串，並套用預設行為。  
  
## <a name="locking-behavior"></a>鎖定行為  
**dwloader**鎖定行為而有所不同，取決於*load_mode_option*。  
  
-   **附加**– 附加時的建議與最常見的選項。 附加資料載入至暫存資料表。 下面將詳細說明的鎖定。  
  
-   **快速附加**– 快速附加直接載入最後的資料表取得 ExclusiveUpdate 資料表鎖定，且不會使用暫存資料表的唯一模式。  
  
-   **重新載入**– 重新載入至暫存資料表載入資料，並需要暫存資料表和最後一個資料表的獨佔鎖定。 不建議重新載入之並行作業。  
  
-   **upsert** – Upsert 資料載入暫存資料表中，並再執行合併作業從臨時區域資料表至最後的資料表。 Upsert 不需要在最後的資料表上的獨佔鎖定。 使用更新插入時，效能可能會有所不同。 測試您的環境中的行為。  
  
### <a name="locking-behavior"></a>鎖定行為  
**附加模式鎖定**  
  
附加可以執行多個交易式模式 （使用-m 引數），但它並不安全的交易。 因此附加應該做為交易式的作業 （不使用 – m 引數）。 不幸的是，最後一個 INSERT SELECT 作業期間，交易式模式低於目前六倍的多重交易模式。  
  
附加模式在兩個階段中載入資料。 第一階段資料載入從來源檔案的暫存資料表同時 （分散可能會發生）。 階段二到最後的資料表從暫存資料表載入資料。 第二個階段執行**INSERT INTO...選取 WITH (TABLOCK)**作業。 下表顯示在最後的資料表上的鎖定行為，並使用時，記錄行為附加模式：  
  
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
  
上述表格顯示**dwloader**使用 append 模式載入堆積或叢集的索引 (CI) 資料表時，不論多重交易式的旗標，並載入至空的資料表或非空白資料表。 鎖定和記錄的每個此類負載組合的行為會顯示在資料表中。 比方說，載入含有 append 模式 (2) 的階段到叢集索引，但不多交易式模式和空資料表將會在資料表上建立的獨佔鎖定的 PDW 且是最小的記錄。 這表示客戶將無法將空的資料表同時載入 （第 2 個） 的階段和查詢。 不過，載入時以相同的組態至非空白資料表，PDW 將不會發行資料表的獨佔鎖定，且並行存取。 不幸的是，完整記錄時，會讓處理程序變。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-dwloader-example"></a>A. 簡單 dwloader 範例  
下列範例示範的起始**載入器**只選取了所需選項。 其他選項會從全域組態檔中，擷取*loadparamfile.txt*。  
  
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
  
使用引數的原始程式檔和錯誤檔的範例。  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>B. 將資料載入至 AdventureWorks 資料表  
下列範例會將資料載入的批次指令碼屬於**AdventureWorksPDW2012**。  若要檢視完整的指令碼，請開啟 aw_create.bat 檔案隨附於**AdventureWorksPDW2012**安裝套件。 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

下列指令碼片段會將資料載入到 DimAccount 和 DimCurrency 資料表使用 dwloader。 此指令碼會使用乙太網路位址。 如果使用 InfiniBand，伺服器將*< appliance_name >*`-SQLCTL01`。  
  
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
  
以下是用於 DimAccount 資料表的 DDL。  
  
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
  
以下是範例資料檔，DimAccount.txt，包含要載入資料表 DimAccount 資料。  
  
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
  
### <a name="c-load-data-from-the-command-line"></a>C. 從命令列將資料載入  
範例 B 中的指令碼可以取代命令列上輸入所有參數，如下列範例所示。  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe –S <Control node IP> -E –M reload –e UTF16 -i .\DimAccount.txt –T AdventureWorksPDW2012.dbo.DimAccount –R DimAccount.bad –t "|" –r \r\n –U <login> -P <password>  
```  
  
命令列參數的描述：  
  
-   *C:\Program Files\Microsoft SQL Server 平行資料 Warehouse\100\dwloader.exe* dwloader.exe 的安裝位置。  
  
-   *-S*後面的控制節點的 IP 位址。  
  
-   *-E*指定載入為 NULL 的空字串。  
  
-   *-M 重新載入*指定截斷目的地資料表，才能將來源資料。  
  
-   *-e UTF16*指出原始程式檔使用的小的位元組由小到大字元編碼類型。  
  
-   *-i.\DimAccount.txt*指定的資料是稱為 DimAccount.txt 存在目前目錄中的檔案。  
  
-   *-T AdventureWorksPDW2012.dbo.DimAccount*指定要接收資料之資料表的 3 組件名稱。  
  
-   *-R DimAccount.bad*指定將寫入檔案，稱為 DimAccount.bad 無法載入的資料列。  
  
-   *– t"|"*指出輸入檔 DimAccount.txt 中的欄位會以縱線字元分隔。  
  
-   *-r \r\n*指定 DimAccount.txt 中的每個資料列的結尾是歸位字元和換行字元。  
  
-   *-U < >-P login_name <password>* 指定的登入和密碼登入具有權限來執行負載。  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
  
