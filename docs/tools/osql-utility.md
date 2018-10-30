---
title: osql 公用程式 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- statements [SQL Server], command prompt
- QUIT command
- Transact-SQL statements, command prompt
- EXIT command
- operating systems [SQL Server], commands
- osql utility [SQL Server]
- stored procedures [SQL Server], command prompt
- scripts [SQL Server], command prompt
- RESET command
- GO command
- command prompt utilities [SQL Server], osql
- CTRL+C command
ms.assetid: cf530d9e-0609-4528-8975-ab8e08e40b9a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: b2f6a7406fb500f3e909761c4c632587748c1df8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47847469"
---
# <a name="osql-utility"></a>osql 公用程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  **osql** 公用程式可讓您輸入 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式、系統程序和指令碼檔案。 這個公用程式利用 ODBC 來與伺服器通訊。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的未來版本將移除此功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 改用 **sqlcmd** 。 如需詳細資訊，請參閱 [sqlcmd Utility](../tools/sqlcmd-utility.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
osql  
[-?] |  
[-L] |  
[  
  {  
     {-Ulogin_id [-Ppassword]} | –E }  
     [-Sserver_name[\instance_name]] [-Hwksta_name] [-ddb_name]  
     [-ltime_out] [-ttime_out] [-hheaders]  
     [-scol_separator] [-wcolumn_width] [-apacket_size]  
     [-e] [-I] [-D data_source_name]  
     [-ccmd_end] [-q "query"] [-Q"query"]  
     [-n] [-merror_level] [-r {0 | 1}]  
     [-iinput_file] [-ooutput_file] [-p]  
     [-b] [-u] [-R] [-O]  
]  
```  
  
## <a name="arguments"></a>引數  
 **-?**  
 顯示 **osql** 參數的語法摘要。  
  
 **-L**  
 列出設定在本機的伺服器，以及在網路中進行廣播的伺服器名稱。  
  
> [!NOTE]  
>  由於網路廣播的本質，因此 **osql** 可能不會收到所有伺服器的及時回應。 因此，這個選項各次的引動過程，傳回的伺服器清單可能各不相同。  
  
 **-U** *login_id*  
 這是使用者登入識別碼。 登入識別碼會區分大小寫。  
  
 **-P** *password*  
 這是一個使用者指定的密碼。 若未使用 **-P** 選項，則 **osql** 會提示輸入密碼。 若在命令提示字元的尾端使用 **-P** 選項且無任何密碼，則 **osql** 會使用預設密碼 (NULL)。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。 如需詳細資訊，請參閱 [Strong Passwords](../relational-databases/security/strong-passwords.md)。  
  
 密碼會區分大小寫。  
  
 OSQLPASSWORD 環境變數可讓您設定目前工作階段的預設密碼。 因此，您不需要將密碼寫在批次檔中。  
  
 若您未使用 **-P** 選項指定密碼，則 **osql** 會先檢查 OSQLPASSWORD 變數。 若未設定任何值，則 **osql** 會使用預設密碼 NULL。 下列範例會在命令提示字元設定 OSQLPASSWORD 變數，然後再存取 **osql** 公用程式：  
  
```  
C:\>SET OSQLPASSWORD=abracadabra  
C:\>osql   
```  
  
> [!IMPORTANT]  
>  若要遮罩您的密碼，請勿連同 **-P** 選項指定 **-U** 選項。 而是改為在搭配 **-U** 選項及其他參數 (不指定 **-P** ) 指定 **osql**後，按下 ENTER，接著 **osql** 就會提示您輸入密碼。 這個方法可確保在輸入密碼時，遮罩您的密碼。  
  
 **-E**  
 使用信任連接，不要求密碼。  
  
 **-S** _伺服器\_名稱_[ **\\**_執行個體\_名稱_]  
 指定要連接的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體。 指定 *server_name* ，即可連接至該伺服器上之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的預設執行個體。 指定 _server\_name_**\\**_instance\_name_，即可連線到該伺服器上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的具名執行個體。 若未指定伺服器，則 **osql** 會連接到本機電腦的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 預設執行個體。 從網路中的遠端電腦執行 **osql** 時，需要使用此選項。  
  
 **-H** *wksta_name*  
 這是一個工作站名稱。 工作站名稱儲存在 **sysprocesses.hostname** 中， **sp_who**會顯示它。 如果未指定這個選項，就會假設目前的電腦名稱。  
  
 **-d** *db_name*  
 啟動 *osql* 時發出 USE **db_name**陳述式。  
  
 **-l** *time_out*  
 指定 **osql** 登入逾時之前的秒數。**osql** 的預設登入逾時值是八秒。  
  
 **-t** *time_out*  
 指定命令逾時之前的秒數。如果未指定 *time_out* 值，命令不會逾時。  
  
 **-h** *headers*  
 指定資料行標頭之間所要列印的資料列數。 預設值是每一組查詢結果各列印一次標頭。 請利用 -1 來指定不列印任何標頭。 若使用 –1，則參數和設定之間不能有空格 (**-h-1**而非 **-h -1**)。  
  
 **-s** *col_separator*  
 指定資料行分隔字元，依預設，它是一個空格。 若要使用對作業系統有特殊意義的字元 ( 如 | ; & < >)，請用雙引號 (") 括住該字元。  
  
 **-w** *column_width*  
 可讓使用者設定輸出的螢幕寬度。 預設值是 80 個字元。 當輸出行到達最大螢幕寬度時，它會折成多行。  
  
 **-a** *packet_size*  
 可讓您要求不同大小的封包。 *packet_size* 的有效值為 512 到 65535。 預設值 **osql** 為伺服器預設值。 增加的封包大小可加強較大指令碼執行 (其中 GO 命令之間的 SQL 陳述式數量很大) 的效能。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 測試指出 8192 通常是大量複製作業的最快設定。 您可以要求較大的封包，但如果無法授與要求，則 **osql** 會預設為伺服器預設值。  
  
 **-e**  
 回應輸入。  
  
 **-I**  
 將 QUOTED_IDENTIFIER 連接選項設為開啟。  
  
 **-D** *data_source_name*  
 連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的 ODBC 驅動程式所定義的 ODBC 資料來源。 **osql** 連接會使用資料來源所指定的選項。  
  
> [!NOTE]  
>  這個選項不會使用定義給其他驅動程式的資料來源。  
  
 **-c** *cmd_end*  
 指定命令結束字元。 依預設，在一行中單獨輸入 GO，便會終止命令，並將命令傳給 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 當您重設命令結束字元時，請勿使用對作業系統有特殊意義的 [!INCLUDE[tsql](../includes/tsql-md.md)] 保留字或字元，不論前面是否附加了反斜線，都是一樣。  
  
 **-q "查詢** ****"**  
 啟動 **osql** 時便執行查詢，但查詢完成時 **osql** 不會結束。 (請注意，查詢陳述式不應包含 GO)。 如果您是從批次檔中發出查詢，請使用變數 (%variables) 或環境變數 (%variables%)。 例如：  
  
```  
SET table=sys.objects  
osql -E -q "select name, object_id from %table%"  
```  
  
 請利用雙引號括住查詢，利用單引號括住內嵌在查詢中的任何項目。  
  
 **-Q"查詢** ****"**  
 執行查詢並立即結束 **osql**。 請利用雙引號括住查詢，利用單引號括住內嵌在查詢中的任何項目。  
  
 **-n**  
 從輸入行中，移除編號和提示符號 (>)。  
  
 **-m** *error_level*  
 自訂錯誤訊息的顯示畫面。 在指定嚴重性層級或以上的錯誤，會顯示訊息編號、狀態和錯誤層級。 在指定層級以下的錯誤不會顯示任何資訊。 請利用 **-1** 來指定訊息傳回所有標頭，即使參考訊息也是如此。 若使用 **-1**，則參數與設定之間不能有空格 (**-m-1**而非 **-m -1**)。  
  
 **-r** { **0**| **1**}  
 將訊息輸出重新導向至畫面 (**stderr**)。 如果您沒有指定參數，或您指定 **0**，便只會重新導向嚴重性層級 11 或以上的錯誤訊息。 如果您指定 **1**，便會重新導向所有訊息輸出 (包括 "print")。  
  
 **-i** *input_file*  
 識別包含 SQL 陳述式或預存程序的批次之檔案。 小於 (**\<**) 比較運算子可用來代替 **-i**。  
  
 **-o** *output_file*  
 識別用來接收 **osql**輸出的檔案。 大於 (**>**) 比較運算子可用來代替 **-o**。  
  
 若 *input_file* 不是 Unicode 且未指定 **-u** ，則會以 OEM 格式儲存 *output_file* 。 若 *input_file* 是 Unicode 或指定 **-u** ，則會以 Unicode 格式儲存 *output_file* 。  
  
 **-p**  
 列印效能統計資料。  
  
 **-b**  
 指定在發生錯誤時， **osql** 會結束作業並傳回 DOS ERRORLEVEL 值。 當 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 錯誤訊息的嚴重性層級大於或等於 11 時，傳回 DOS ERRORLEVEL 變數的值是 1；否則，傳回的值是 0。 [!INCLUDE[msCoName](../includes/msconame-md.md)] MS-DOS 批次檔可以測試 DOS ERRORLEVEL 的值，而且能夠適當處理錯誤。  
  
 **-u**  
 指定無論 *input_file* 的格式為何， *output_file*均以 Unicode 格式儲存。  
  
 **-R**  
 指定在將貨幣、日期和時間資料轉換成字元資料時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ODBC 驅動程式要使用用戶端設定。  
  
 **-O**  
 指定停用某些 **osql** 功能，以符合舊版 **isql**的行為。 停用的功能如下：  
  
-   EOF 批次處理  
  
-   自動調整主控台寬度  
  
-   寬字訊息  
  
 它也會將預設的 DOS ERRORLEVEL 值設為 -1。  
  
> [!NOTE]  
>  **osql**已不再支援 **-n** 、 **-O** 和 **-D**選項。  
  
## <a name="remarks"></a>Remarks  
 **osql** 公用程式會在已設定此處所列之區分大小寫選項的情況下，直接從作業系統中啟動。 啟動 **osql**後，其會接受 SQL 陳述式並以互動方式傳送至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 結果會格式化，顯示在畫面中 (**stdout**)。 使用 QUIT 或 EXIT 來結束 **osql**。  
  
 若您在啟動 **osql**時未指定使用者名稱，則 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會檢查及使用類似 **osqluser=(**_user_**)** 或 **osqlserver=(**_server_**)** 等環境變數。 如果未設定任何環境變數，就會使用工作站使用者名稱。 如果您沒有指定伺服器，就會使用工作站的名稱。  
  
 若 **-U** 或 **-P** 選項皆未使用，則 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會嘗試使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 驗證模式執行連接。 這項驗證是以執行 [!INCLUDE[msCoName](../includes/msconame-md.md)] osql **使用者的**Windows 帳戶為基礎。  
  
 **osql** 公用程式會使用 ODBC API。 這個公用程式使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ISO 連接選項的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ODBC 驅動程式預設值。 如需詳細資訊，請參閱＜ANSI 選項的作用＞。  
  
> [!NOTE]  
>  **osql** 公用程式不支援 CLR 使用者定義資料類型。 若要處理這些資料類型，您必須使用 **sqlcmd** 公用程式。 如需詳細資訊，請參閱 [sqlcmd Utility](../tools/sqlcmd-utility.md)。  
  
## <a name="osql-commands"></a>OSQL 命令  
 除了 [!INCLUDE[tsql](../includes/tsql-md.md)] osql **內的**陳述式，您也可以使用這些命令。  
  
|命令|Description|  
|-------------|-----------------|  
|GO|執行在上一個 GO 之後輸入的所有陳述式。|  
|RESET|清除您已輸入的任何陳述式。|  
|QUIT 或 EXIT( )|結束 **osql**。|  
|CTRL+C|結束查詢，但不結束 **osql**。|  
  
> [!NOTE]  
>  !! 和 ED 命令不再受到 **osql**支援。  
  
 命令結束字元 GO (預設)、RESET EXIT、QUIT 和 CTRL+C 必須在行首並緊接在 **osql** 提示之後，才能夠辨識。  
  
 GO 會發出批次結束及執行任何快取的 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式的信號。 您在每個輸入行結束而按下 ENTER 時， **osql** 會快取這一行的陳述式。 當您在輸入 GO 之後按下 ENTER 鍵時，會將目前所快取的所有陳述式做為單一批次傳給 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
 目前 **osql** 公用程式的運作方式，如同在任何執行的指令碼尾端有隱含的 GO，因此會執行指令碼中的所有陳述式。  
  
 請在行首輸入命令結束字元來結束命令。 您可以在命令結束字元之後，輸入一個整數來指定命令應該執行的次數。 例如，若要執行這個命令 100 次，請輸入：  
  
```  
SELECT x = 1  
GO 100  
```  
  
 執行結束時，會列印結果一次。 **osql** 不接受每行超出 1,000 個字元。 大型陳述式應該分成幾行。  
  
 Windows 的命令重新呼叫功能可用來重新呼叫及修改 **osql** 陳述式。 您可以輸入 RESET 來清除現有的查詢緩衝區。  
  
 執行預存程序時， **osql** 會在批次的各組結果之間，列印一空白行。 另外，當「0 個資料列受影響」的訊息不適合執行的陳述式時，便不會出現這則訊息。  
  
## <a name="using-osql-interactively"></a>以互動方式使用 osql  
 若要以互動方式來使用 **osql** ，請在命令提示字元之下，輸入 **osql** 命令 (及任何選項)。  
  
 您可以輸入類似下列的命令來讀取包含查詢 (如 Stores.qry) 的檔案，供 **osql** 執行：  
  
```  
osql -E -i stores.qry  
```  
  
 您可以輸入類似下列中的命令來讀取包含查詢 (如 Titles.qry) 的檔案，以及將結果導向另一個檔案：  
  
```  
osql -E -i titles.qry -o titles.res  
```  
  
> [!IMPORTANT]  
>  可能的話，請使用 **-E**選項 (信任連接)。  
  
 當以互動方式使用 **osql** 時，您可以使用 **:r**_file\_name_，將作業系統檔案讀入命令緩衝區中。 這會將 *file_name* 中的 SQL 指令碼當作單一批次直接傳給伺服器。  
  
> [!NOTE]  
>  當使用 **osql**時，如果批次分隔字元 GO 出現在 SQL 指令碼檔案中， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會將其視為語法錯誤。  
  
## <a name="inserting-comments"></a>插入註解  
 您可以在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] osql **提交給**的 Transact-SQL 陳述式中併入註解。 可用的註解樣式有兩種：-- 和 /*...\*/。  
  
## <a name="using-exit-to-return-results-in-osql"></a>在 osql 中利用 EXIT 傳回結果  
 您可以利用 SELECT 陳述式的結果來做為 **osql**的傳回值。 如果為數值，則最後一個結果資料列的最後一個資料行會轉換成 4 位元組的整數 (long)。 MS-DOS 會將低位元組傳給父處理序或作業系統錯誤層級。 Windows 會傳遞整個 4 位元組整數。 語法如下：  
  
```  
EXIT ( < query > )  
```  
  
 例如：  
  
```  
EXIT(SELECT @@ROWCOUNT)  
```  
  
 您也可以將 EXIT 參數併入批次檔中。 例如：  
  
```  
osql -E -Q "EXIT(SELECT COUNT(*) FROM '%1')"  
```  
  
 **osql** 公用程式會將 **()** 括號之間的任何內容，完全照原本輸入的內容傳給伺服器。 如果預存的系統程序選取某一組，傳回某個值，此時只會傳回選取的項目。 括號之間沒有任何內容的 EXIT **()** 陳述式，會執行批次中在它前面的任何內容，之後，便結束作業，不傳回任何值。  
  
 EXIT 有四種格式：  
  
-   EXIT  
  
> [!NOTE]  
>  不執行批次；立即結束，不傳回任何值。  
  
-   EXIT **()**  
  
> [!NOTE]  
>  執行批次之後，便結束作業，不傳回任何值。  
  
-   EXIT **(**_query_**)**  
  
> [!NOTE]  
>  執行包含查詢的批次，傳回查詢結果之後，便告結束。  
  
-   狀態為 127 的 RAISERROR  
  
> [!NOTE]  
>  若在 **osql** 指令碼內使用 RAISERROR，且產生 127 狀態，則 **osql** 會結束作業，且會將訊息識別碼傳回用戶端。 例如：  
  
```  
RAISERROR(50001, 10, 127)  
```  
  
 此錯誤會使得 **osql** 指令碼結束作業，並將訊息識別碼 50001 傳回用戶端。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]保留傳回值 -1 至 -99； **osql** 定義了下列值：  
  
-   -100  
  
     在選取傳回值之前發生錯誤。  
  
-   -101  
  
     在選取傳回值時，找不到任何資料列。  
  
-   -102  
  
     在選取傳回值時，發生轉換錯誤。  
  
## <a name="displaying-money-and-smallmoney-data-types"></a>顯示 money 和 smallmoney 資料類型  
 **osql** 會顯示兩位數的 **money** 和 **smallmoney** 資料類型，不過， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會在內部利用四位數來儲存這個值。 請設想下列範例：  
  
```  
SELECT CAST(CAST(10.3496 AS money) AS decimal(6, 4))  
GO  
```  
  
 這個陳述式會產生 `10.3496`的結果，這表示在儲存值時，所有小數點保留不動。  
  
## <a name="see-also"></a>另請參閱  
 [註解 &#40;MDX&#41;](../mdx/comment-mdx.md)   
 [-- &#40;註解&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)   
 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../t-sql/functions/cast-and-convert-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
