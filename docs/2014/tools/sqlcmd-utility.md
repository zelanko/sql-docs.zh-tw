---
title: sqlcmd 公用程式 | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- statements [SQL Server], command prompt
- QUIT command
- Transact-SQL statements, command prompt
- EXIT command
- sqlcmd commands
- ED command
- sqlcmd utility
- command prompt utilities [SQL Server], sqlcmd
- '!! command'
- stored procedures [SQL Server], command prompt
- system stored procedures [SQL Server], command prompt
- sqlcmd utility, about sqlcmd utility
- scripts [SQL Server], command prompt
- RESET command
- GO command
ms.assetid: e1728707-5215-4c04-8320-e36f161b834a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d128085012c0ef3a9bc58b147f982a26d2c094b8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63035380"
---
# <a name="sqlcmd-utility"></a>sqlcmd 公用程式
  公用程式可讓您[!INCLUDE[tsql](../includes/tsql-md.md)]在命令提示字元處、在 SQLCMD 模式的 [**查詢編輯器**] 中、在 Windows 腳本檔案中，或是在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 作業的作業系統（cmd.exe）作業步驟中，輸入語句、系統程式和腳本檔案。 `sqlcmd` 這個公用程式利用 ODBC 執行 [!INCLUDE[tsql](../includes/tsql-md.md)] 批次。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]在 [ [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]**查詢編輯器**] 中使用 SqlClient 執行一般和 SQLCMD 模式。 從命令列執行 `sqlcmd` 時，`sqlcmd` 會使用 ODBC 驅動程式。 因為可能會套用不同的預設選項，因此，以 SQLCMD 模式在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中以及在 `sqlcmd` 公用程式中執行相同的查詢時，可能會看到不同的行為。  
  
 目前，`sqlcmd` 不需要在命令列選項與值之間保留一個空格。 但是在未來的版本中，可能會需要在命令列選項與值之間空一個空格。  
  
## <a name="syntax"></a>語法  
  
```  
  
   sqlcmd  
   -a  
   packet_size  
   -A (dedicated administrator connection)  
-b (terminate batch job if there is an error)  
-cbatch_terminator-C (trust the server certificate)  
-ddb_name-e (echo input)  
-E (use trusted connection)  
-fcodepage | i:codepage[,o:codepage] | o:codepage[,i:codepage]  
-hrows_per_header-Hworkstation_name-iinput_file-I (enable quoted identifiers)  
-k[1 | 2] (remove or replace control characters)  
-Kapplication_intent-llogin_timeout-L[c] (list servers, optional clean output)  
-merror_level-Mmultisubnet_failover-N (encrypt connection)  
-ooutput_file-p[1] (print statistics, optional colon format)  
-Ppassword-q "cmdline query"-Q "cmdline query" (and exit)  
-r[0 | 1] (msgs to stderr)  
-R (use client regional settings)  
-scol_separator-S [protocol:]server[\instance_name][,port]  
-tquery_timeout-u (unicode output file)  
-Ulogin_id-vvar = "value"-Verror_severity_level-wcolumn_width-W (remove trailing spaces)  
-x (disable variable substitution)  
-X[1] (disable commands, startup script, environment variables and optional exit)  
-yvariable_length_type_display_width-Yfixed_length_type_display_width-znew_password -Znew_password (and exit)  
  
-? (usage)  
```  
  
## <a name="command-line-options"></a>命令列選項  
 **登入相關選項**  
  **-A**  
 利用專用管理員連接 (DAC) 來登入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 這種連接可用以進行伺服器的疑難排解。 只有在支援 DAC 的伺服器電腦上才可進行。 如果無法使用 DAC，`sqlcmd` 會產生一則錯誤訊息，並結束作業。 如需有關 DAC 的詳細資訊，請參閱 [資料庫管理員的診斷連線](../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)。  
  
 **-C**  
 這個參數由用戶端所設定，以隱含方式信任伺服器憑證而且不進行驗證。 這個選項相當於 ADO.NET 選項 `TRUSTSERVERCERTIFICATE = true`。  
  
 **-d** _db_name_  
 當您`USE`啟動`sqlcmd`時，會發出*db_name*的語句。 這個選項會設定 `sqlcmd` 指令碼變數 SQLCMDDBNAME。 這會指定初始資料庫。 預設值為您登入的預設資料庫屬性。 如果資料庫不存在，會產生一則錯誤訊息，且會結束 `sqlcmd`。  
  
 **-l** _login_timeout_  
 指定在您嘗試連接到伺服器時，ODBC 驅動程式之 `sqlcmd` 登入逾時之前的秒數。 這個選項會設定 `sqlcmd` 指令碼變數 SQLCMDLOGINTIMEOUT。 
  `sqlcmd` 的預設登入逾時值是 8 秒。 此登入逾時必須是介於 0 和 65534 之間的數字。 如果所提供的值不是數值或不在該範圍內，`sqlcmd` 就會產生錯誤訊息。 0 值指定逾時值無限。  
  
 **-E**  
 使用信任連接登入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，而不用使用者名稱和密碼。 根據預設，如果沒有指定 -E，`sqlcmd` 會使用信任連接選項。  
  
 
  **-E** 選項會忽略可能出現的使用者名稱與密碼環境變數設定，例如 SQLCMDPASSWORD。 如果同時使用 **-E** 選項和 **-U** 或 **-P** 選項，就會產生錯誤訊息。  
  
 **-H** _workstation_name_  
 這是工作站名稱。 這個選項會設定 `sqlcmd` 指令碼變數 SQLCMDWORKSTATION。 工作站名稱列在 **sys.processes** 目錄檢視的 **hostname** 資料行中，而且可以使用預存程序 **sp_who** 傳回名稱。 如果未指定這個選項，預設值為目前的電腦名稱。 這個名稱可用來識別不同的 `sqlcmd` 工作階段。  
  
 **-K** _application_intent_  
 宣告連接到伺服器時的應用程式工作負載類型。 目前唯一支援的值是 **ReadOnly**。 若未指定 **-K**，sqlcmd 公用程式將無法支援 AlwaysOn 可用性群組中連接至次要複本。 如需詳細資訊，請參閱使用中[次要資料庫：可讀取的次要複本](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)。  
  
 `-M`*multisubnet_failover*  
 在連接到 `-M` 可用性群組的可用性群組接聽程式或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體時，永遠指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 
  `-M` 提供目前使用中伺服器的更快速偵測與連接。 如果未指定 `-M`，`-M` 為關閉。 如需的詳細[!INCLUDE[ssHADR](../includes/sshadr-md.md)]資訊，請參閱[可用性群組接聽程式、用戶端連線性和應用程式容錯移轉 &#40;SQL Server&#41;](../database-engine/listeners-client-connectivity-application-failover.md)、[建立和設定可用性群組 &#40;SQL Server ](../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)&#41;、[容錯移轉叢集和 AlwaysOn 可用性群組 &#40;](../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)SQL Server&#41;和作用中[次要複本：可讀取的次要複本](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)。  
  
 **-N**  
 用戶端會用這個參數要求加密的連接。  
  
 **-P** _密碼_  
 這是一個使用者指定的密碼。 密碼會區分大小寫。 如果使用-U 選項，但未使用 **-P**選項，且未設定 SQLCMDPASSWORD 環境變數， `sqlcmd`則會提示使用者輸入密碼。 如果在沒有密碼`sqlcmd`的情況下，于命令提示字元的結尾使用 **-P**選項，則會使用預設密碼（Null）。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。 如需詳細資訊，請參閱 [增強式密碼](../relational-databases/security/strong-passwords.md)。  
  
 密碼提示的顯示方式，會以將密碼提示輸出到主控台的方式顯示，如： `Password:`  
  
 使用者輸入為隱藏狀態。 這表示畫面上不會顯示任何內容，而且游標也不會移動。  
  
 SQLCMDPASSWORD 環境變數可讓您設定目前工作階段的預設密碼。 因此，您不需要將密碼寫在批次檔中。  
  
 下列範例會先在命令提示字元處設定 SQLCMDPASSWORD 變數，再存取 `sqlcmd` 公用程式。 在命令提示字元中，輸入：  
  
 `SET SQLCMDPASSWORD= p@a$$w0rd`  
  
> [!IMPORTANT]  
>  任何能夠見到您的電腦監視器的人，都能夠見到密碼。  
  
 請在下列命令提示字元之下，輸入：  
  
 `sqlcmd`  
  
 如果使用者名稱和密碼的組合不正確，會產生錯誤訊息。  
  
> [!NOTE]  
>  保留 OSQLPASSWORD 環境變數的目的是為了與舊版相容。 SQLCMDPASSWORD 環境變數優先于 OSQLPASSWORD 環境變數;這表示`sqlcmd`和**osql**可以在彼此不受干擾的情況下使用，而且舊的腳本仍會繼續工作。  
  
 如果同時使用 **-P** 選項和 **-E** 選項，就會產生錯誤訊息。  
  
 如果 **-P** 選項後面有多個引數，便會產生錯誤訊息，而且程式將會結束。  
  
 **-S** [*通訊協定*：*] 伺服器*[**\\**_instance_name_] [**，**_埠_]  
 指定要連接的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體。 它會設定 `sqlcmd` 指令碼變數 SQLCMDSERVER。  
  
 指定 *server_name*，即可連接至該伺服器電腦上之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的預設執行個體。 指定*server_name* [ **\\** _instance_name_ ]，以連接到該伺服器電腦[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上的已命名實例。 如果未指定伺服器電腦，`sqlcmd` 會連接到本機電腦上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的預設執行個體。 當您從網路的遠端電腦執行 `sqlcmd` 時，需要這個選項。  
  
 *通訊協定*可以`tcp`是（tcp/ip）、 `lpc` （共用記憶體）或`np` （具名管道）。  
  
 如果您在啟動`sqlcmd`時未[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]指定*server_name* [ **\\** _instance_name_ ]，會檢查並使用 SQLCMDSERVER 環境變數。  
  
> [!NOTE]  
>  保留 OSQLSERVER 環境變數的目的是為了與舊版相容。 SQLCMDSERVER 環境變數優先于 OSQLSERVER 環境變數;這表示`sqlcmd`和**osql**可以在彼此不受干擾的情況下使用，而且舊的腳本仍會繼續工作。  
  
 **-U** _login_id_  
 這是使用者登入識別碼。  
  
> [!NOTE]  
>  可利用 OSQLUSER 環境變數達到回溯相容性。 SQLCMDUSER 環境變數優先於 OSQLUSER 環境變數。 這表示您`sqlcmd`可以在彼此旁使用和**osql** ，而不會互相干擾。 這也表示現有的 **osql** 指令碼仍然有效。  
  
 如果沒有指定 **-U**選項或 **-P**選項， `sqlcmd`則會嘗試使用[!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 驗證模式進行連接。 這項驗證以執行 `sqlcmd` 之使用者的 Windows 帳戶為基礎。  
  
 如果同時使用 **-U** 選項和 **-E** 選項 (本主題稍後將說明)，便會產生錯誤訊息。 如果 **-U** 選項後面有多個引數，就會產生錯誤訊息並結束程式。  
  
 **-z** _new_password_  
 變更密碼：  
  
 `sqlcmd -U someuser -P s0mep@ssword -z a_new_p@a$$w0rd`  
  
 **-Z** _new_password_  
 變更密碼並結束：  
  
 `sqlcmd -U someuser -P s0mep@ssword -Z a_new_p@a$$w0rd`  
  
 **輸入/輸出選項**  
  **-f** _字碼頁_ | **i：**_字碼頁_[**，o：**_字碼頁_] |**o：**_字碼頁_[**，i：**_字碼頁_]  
 指定輸入和輸出字碼頁。 字碼頁碼是一個數值，指定已安裝的 Windows 字碼頁。  
  
 字碼頁轉換規則：  
  
-   如果未指定字碼頁，則 `sqlcmd` 會在輸入檔和輸出檔中使用目前的字碼頁，除非輸入檔是 Unicode 檔，否則就不需要轉換。  
  
-   
  `sqlcmd` 會自動識別位元組由大到小 (Big-Endian) 和位元組由小到大 (Little-Endian) 的 Unicode 輸入檔。 如果已指定 **-u** 選項，則輸出一律為位元組由小到大的 Unicode。  
  
-   如果未指定輸出檔，則輸出字碼頁會是主控台字碼頁。 這可讓輸出正確地顯示在主控台上。  
  
-   假設多個輸入檔都是相同的字碼頁。 Unicode 與非 Unicode 的輸入檔可以混合使用。  
  
 在命令提示字元下輸入 `chcp`，以驗證 Cmd.exe 的字碼頁。  
  
 **-i** _input_file_[**，**_input_file2_...]  
 識別包含 SQL 陳述式或預存程序的批次之檔案。 您可以指定多個檔案，它們會依照順序加以讀取和處理。 檔案名稱之間不能有空格。 
  `sqlcmd` 會先檢查指定的檔案是否全部存在。 如果有一個或多個檔案不存在，`sqlcmd` 會結束作業。 -i 和 -Q/-q 為互斥選項。  
  
 路徑範例：  
  
 **-i**C：\\<檔案名\>  
  
 **-i** \\ \\<Server\> \\<共用 $>\\<檔案名\>  
  
 **-i**「C:\Some 資料夾\\<檔案名\>」  
  
 包含空格的檔案路徑必須用引號括住。  
  
 這個選項可以使用一次以上： **-i**_input_file_ **-I**_I input_file_。  
  
 **-o** _output_file_  
 識別用來接收 `sqlcmd` 輸出的檔案。  
  
 如果指定 **-u** ， *output_file* 會以 Unicode 格式儲存。 如果檔案名稱無效，會產生一則錯誤訊息，且會結束 `sqlcmd`。 
  `sqlcmd` 不支援同時將多個 `sqlcmd` 處理序寫入相同的檔案。 檔案輸出會損毀或不正確。 如需檔案格式的詳細資訊，請參閱 **-f** 參數。 如果不存在，則會建立這個檔案。 並覆寫先前 `sqlcmd` 工作階段所產生的同名檔案。 此處所指定的檔案並不是 **stdout** 檔案。 如果指定 **stdout** 檔案，則不會使用這個檔案。  
  
 路徑範例：  
  
 **-o**C：\\< filename>  
  
 **-o** \\ \\<Server\> \\<Share $>\\<檔案名\>  
  
 **-o "** C:\Some 資料夾\\<檔案名\>」  
  
 包含空格的檔案路徑必須用引號括住。  
  
 **-r**[**0** | **1**]  
 將錯誤訊息輸出重新導向至畫面 (**stderr**)。 如果您沒有指定參數，或指定 **0**，只會重新導向嚴重性層級 11 (含) 以上的錯誤訊息。 如果您指定 **1**，便會重新導向包括 PRINT 在內的所有錯誤訊息輸出。 如果您使用 -o，不會有任何作用。 根據預設，訊息會傳送到 **stdout**。  
  
 **-R**  
 會`sqlcmd`根據用戶端的地區設定，將從抓取的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]數值、貨幣、日期和時間資料行當地語系化。 根據預設，這些資料行會使用伺服器的地區設定來顯示。  
  
 **-u**  
 指定無論 *input_file* 的格式為何， *output_file*均以 Unicode 格式儲存。  
  
 **查詢執行選項**  
  **-e**  
 將輸入指令碼寫入標準的輸出裝置 (**stdout**) 中。  
  
 **-I**  
 將 SET QUOTED_IDENTIFIER 連接選項設為 ON。 依預設，此選項設定為 OFF。 如需詳細資訊，請參閱[SET QUOTED_IDENTIFIER &#40;transact-sql&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql)。  
  
 **-q "** _cmdline query_ **"**  
 當 `sqlcmd` 啟動時執行查詢，但查詢結束執行後不要退出 `sqlcmd`。 可以執行多項以分號分隔的查詢。 請依照下列範例所示，利用引號來括住查詢。  
  
 在命令提示字元中，輸入：  
  
 `sqlcmd -d AdventureWorks2012 -q "SELECT FirstName, LastName FROM Person.Person WHERE LastName LIKE 'Whi%';"`  
  
 `sqlcmd -d AdventureWorks2012 -q "SELECT TOP 5 FirstName FROM Person.Person;SELECT TOP 5 LastName FROM Person.Person;"`  
  
> [!IMPORTANT]  
>  請勿在查詢中使用 GO 結束字元。  
  
 如果使用此選項時指定了 `-b`，`sqlcmd` 會發生錯誤，並結束作業。 本主題稍後將說明 `-b`。  
  
 **-Q "** _cmdline query_ **"**  
 啟動 `sqlcmd` 時執行查詢，然後立即退出 `sqlcmd`。 可以執行多項以分號分隔的查詢。  
  
 請依照下列範例所示，利用引號來括住查詢。  
  
 在命令提示字元中，輸入：  
  
 `sqlcmd -d AdventureWorks2012 -Q "SELECT FirstName, LastName FROM Person.Person WHERE LastName LIKE 'Whi%';"`  
  
 `sqlcmd -d AdventureWorks2012 -Q "SELECT TOP 5 FirstName FROM Person.Person;SELECT TOP 5 LastName FROM Person.Person;"`  
  
> [!IMPORTANT]  
>  請勿在查詢中使用 GO 結束字元。  
  
 如果使用此選項時指定了 `-b`，`sqlcmd` 會發生錯誤，並結束作業。 本主題稍後將說明 `-b`。  
  
 **-t** _query_timeout_  
 指定命令（或 SQL 語句）超時之前的秒數。此選項會設定`sqlcmd`腳本變數 SQLCMDSTATTIMEOUT。 如果未指定*time_out*值，則命令不會超時。*查詢 * * time_out*必須是介於1到65534之間的數位。 如果所提供的值不是數值或不在該範圍內，`sqlcmd` 就會產生錯誤訊息。  
  
> [!NOTE]  
>  實際逾時值可能與指定的 *time_out* 值之間有幾秒的差異。  
  
 **-vvar =** _value_[ **var =** _value_...]  
 建立可`sqlcmd`在`sqlcmd`腳本中使用的腳本變數。 如果值包含空格，請用引號括住該值。 您可以指定多個**_var_**=**"*`values`*"** 值。 如果指定的任何值發生錯誤，`sqlcmd` 會產生一則錯誤訊息，並結束作業。  
  
 `sqlcmd -v MyVar1=something MyVar2="some thing"`  
  
 `sqlcmd -v MyVar1=something -v MyVar2="some thing"`  
  
 **-x**  
 讓 `sqlcmd` 忽略指令碼變數。 當指令碼所包含的許多 INSERT 陳述式可能含有與一般變數 (例如 $(*variable_name*)) 相同格式的字串時，這就很有用。  
  
 **格式化選項**  
  **-h** _標頭_  
 指定資料行標頭之間所要列印的資料列數。 預設值是每一組查詢結果各列印一次標頭。 這個選項會設定 `sqlcmd` 指令碼變數 SQLCMDHEADERS。 請利用 **-1** 來指定不列印標頭。 任何無效的值都會讓 `sqlcmd` 產生錯誤訊息，並結束作業。  
  
 **-k** [**1** | **2**]  
 從輸出中移除所有控制字元，如定位字元和新行字元。 這會在資料傳回時，保留資料行的格式。 如果指定 1，會用單一空格來取代控制字元。 如果指定 2，會用單一空格取代連續控制字元。 **-k**與 **-版 k1**相同。  
  
 **-s** _col_separator_  
 指定資料行分隔字元。 預設值是空格。 這個選項會設定 `sqlcmd` 指令碼變數 SQLCMDCOLSEP。 若要使用對作業系統有特殊意義的字元，如連字號 (&) 或分號 (;)，請用引號 (") 括住該字元。 資料行分隔字元可以是任何 8 位元的字元。  
  
 **-w** _column_width_  
 指定輸出的螢幕寬度。 這個選項會設定 `sqlcmd` 指令碼變數 SQLCMDCOLWIDTH。 資料行寬度必須是大於 8 且小於 65536 的數字。 如果指定的資料行寬度不在該範圍內，`sqlcmd` 會產生錯誤訊息。 預設寬度是 80 個字元。 當輸出行超出指定的資料行寬度時，它會折行。  
  
 **-W**  
 這個選項會從資料行中移除尾端的空格。 在準備要匯出至另一個應用程式的資料時，請使用 **-s** 選項與這個選項。 這個選項不能搭配 **-y** 或 **-Y** 選項一起使用。  
  
 **-y** _variable_length_type_display_width_  
 設定 `sqlcmd` 指令碼變數 SQLCMDMAXVARTYPEWIDTH。 預設值是 256。 這會限制大型可變長度資料類型的傳回字元數：  
  
-   `varchar(max)`  
  
-   `nvarchar(max)`  
  
-   `varbinary(max)`  
  
-   `xml`  
  
-   `UDT (user-defined data types)`  
  
-   `text`  
  
-   `ntext`  
  
-   `image`  
  
> [!NOTE]  
>  UDT 可以是固定長度，這會隨著實作情況而不同。 如果固定長度 UDT 的長度小於 *display_width*，傳回的 UDT 值不會受到影響。 不過，如果長度超出 *display_width*，便會截斷輸出。  
  
 
> [!IMPORTANT]  
>  使用 **-y 0** 選項時，要非常小心，因為它可能會讓伺服器和網路出現嚴重的效能問題，這會隨著傳回的資料大小而不同。  
  
 **-Y** _fixed_length_type_display_width_  
 設定 `sqlcmd` 指令碼變數 SQLCMDMAXFIXEDTYPEWIDTH。 預設值是 0 (無限制)。 限制針對下列資料類型傳回的字元數：  
  
-   `char(`*n* `)`，其中 1<= n<= 8000  
  
-   `nchar(n`*n* `)`，其中 1<= n<= 4000  
  
-   `varchar(n`*n* `)`，其中 1<= n<= 8000  
  
-   `nvarchar(n`*n* `)`，其中 1<= n<= 4000  
  
-   `varbinary(n`*n* `)`，其中 1<= n<= 4000  
  
-   `variant`  
  
 **錯誤報表選項**  
  `-b`  
 指定在發生錯誤時，`sqlcmd` 會結束作業並傳回 DOS ERRORLEVEL 值。 當 **錯誤訊息的嚴重性層級大於 10 時，傳回 DOS ERRORLEVEL 變數的值是** 1 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ；否則，傳回的值是 **0**。 如果除了設定 `-V` 以外，還設定了 `-b` 選項，且嚴重性層級低於使用 `sqlcmd` 所設定的值，則 `-V` 不會報告發生錯誤。 命令提示字元批次檔案可以測試 ERRORLEVEL 的值，而且能夠適當地處理錯誤。 
  `sqlcmd` 不會報告嚴重性層級 10 (參考用訊息) 的錯誤。  
  
 如果 `sqlcmd` 指令碼包含不正確的命令、語法錯誤，或遺漏指令碼變數，則傳回的 ERRORLEVEL 便是 1。  
  
 **-m** _error_level_  
 控制哪些錯誤訊息會傳送至 **stdout**。 系統會傳送嚴重性層級大於或等於這個層級的訊息。 當這個值設定為 **-1**時，系統就會傳送包括資訊訊息的所有訊息。 
  **-m** 與 **-1**之間不允許有空格。 例如， **-m-1** 為有效，而 **-m -1** 為無效。  
  
 這個選項也會設定 `sqlcmd` 指令碼變數 SQLCMDERRORLEVEL。 這個變數具有預設值 0。  
  
 `-V`*error_severity_level*  
 控制用來設定 ERRORLEVEL 變數的嚴重性層級。 嚴重性層級大於或等於這個值的錯誤訊息會設定 ERRORLEVEL。 小於 0 的值會回報成 0。 批次和 CMD 檔案可用來測試 ERRORLEVEL 變數的值。  
  
 **其他選項**  
  **-a** _packet_size_  
 要求不同大小的封包。 這個選項會設定 `sqlcmd` 指令碼變數 SQLCMDPACKETSIZE。 *packet_size*必須是介於512和32767之間的值。 預設 = 4096。 較大的封包大小可以讓 GO 命令之間具有許多 SQL 陳述式的指令碼執行得以提高效能。 您可以要求較大的封包。 但是，若要求遭到拒絕，`sqlcmd` 便會使用伺服器預設的封包大小。  
  
 **-c** _batch_terminator_  
 指定批次結束字元。 依預設，在一行中單獨輸入 "GO" 這個字，便會終止命令，並將命令傳給 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 當您重設批次結束字元時，請勿使用對作業系統有特殊意義的 [!INCLUDE[tsql](../includes/tsql-md.md)] 保留關鍵字或字元，即使它們前面附加了反斜線也一樣。  
  
 **-L**[**c**]  
 列出設定在本機的伺服器電腦，以及在網路中進行廣播的伺服器電腦名稱。 這個參數不能結合其他參數來使用。 可以列出的最大伺服器電腦數目為 3000。 如果伺服器清單因為緩衝區的大小而遭到截斷，將會顯示一則警告訊息。  
  
> [!NOTE]  
>  由於網路廣播的本質之故，`sqlcmd` 可能不會收到所有伺服器及時的回應。 因此，這個選項每次的引動過程，所傳回的伺服器清單可能各不相同。  
  
 如果指定了選擇性的參數 **c** ，顯示的輸出不會有 Servers: 標頭行，列出的每個伺服器行也都不會有開頭空白。 這稱為清除輸出。 清除輸出可以增進指令碼語言的處理效能。  
  
 **-p**[**1**]  
 列印每個結果集的效能統計資料。 以下是效能統計資料的格式範例：  
  
 `Network packet size (bytes): n`  
  
 `x xact[s]:`  
  
 `Clock Time (ms.): total       t1  avg       t2 (t3 xacts per sec.)`  
  
 其中：  
  
 
  `x` = [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所處理的交易數目。  
  
 
  `t1` = 所有交易的總時間。  
  
 
  `t2` = 單一交易的平均時間。  
  
 
  `t3` = 每秒的平均交易數。  
  
 所有時間都以毫秒表示。  
  
 如果指定了選擇性參數 **1** ，統計資料的輸出格式是用冒號分隔的格式，很容易匯入試算表中，指令碼也很容易處理它。  
  
 如果選擇性參數是**1**以外的任何值，則會產生錯誤並`sqlcmd`結束。  
  
 `-X`[**1**]  
 停用從批次檔執行 `sqlcmd` 時，可能會危及系統安全性的命令。 仍會辨識停用的命令；`sqlcmd` 會發出一則警告訊息，並繼續作業。 如果指定了選擇性參數**1** ， `sqlcmd`會產生錯誤訊息，然後結束。 使用 `-X` 選項時，會停用下列命令：  
  
-   **ED-24000B**  
  
-   **!!** _命令_  
  
 如果指定了 `-X` 選項，您就無法將環境變數傳給 `sqlcmd`。 也無法執行利用 SQLCMDINI 指令碼變數所指定的啟動指令碼。 如需`sqlcmd`腳本變數的詳細資訊，請參閱搭配[腳本變數使用 sqlcmd](../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)。  
  
 **-?**  
 顯示 `sqlcmd` 選項的語法摘要。  
  
## <a name="remarks"></a>備註  
 您不需要按照語法區段中顯示的順序使用選項。  
  
 傳回多項結果時，`sqlcmd` 會在批次的各結果集之間，列印一行空白行。 此外，當「\<x> 受影響的資料列」訊息不適用於執行的語句時，就不會出現。  
  
 若要`sqlcmd`以互動方式`sqlcmd`使用，請在命令提示字元中，使用本主題稍早所述的一或多個選項來輸入。 如需詳細資訊，請參閱 [使用 sqlcmd 公用程式](../relational-databases/scripting/sqlcmd-use-the-utility.md)  
  
> [!NOTE]  
>  選項 **-L**、 **-Q**、 **-Z**或 **-i**會導致`sqlcmd`在執行之後結束。  
  
 命令列環境 (Cmd.exe) 中之 `sqlcmd` 命令列的總長度 (包括所有引數和擴充的變數)，皆由 Cmd.exe 的作業系統決定。  
  
## <a name="variable-precedence-low-to-high"></a>變數優先順序 (由低至高)  
  
1.  系統層級環境變數  
  
2.  使用者層級環境變數  
  
3.  命令 shell （**set** X = Y）在執行之前于命令提示`sqlcmd`字元中設定。  
  
4.  **sqlcmd-v**X = Y  
  
5.  **： Setvar**X Y  
  
> [!NOTE]  
>  若要檢視環境變數，請在 [控制台] **** 中開啟 [系統] ****，然後按一下 [進階] **** 索引標籤。  
  
## <a name="sqlcmd-scripting-variables"></a>sqlcmd 指令碼變數  
  
|變數|相關參數|R/W|預設|  
|--------------|--------------------|----------|-------------|  
|SQLCMDUSER|-U|R|""|  
|SQLCMDPASSWORD|-P|--|""|  
|SQLCMDSERVER|-S|R|"DefaultLocalInstance"|  
|SQLCMDWORKSTATION|-H|R|"ComputerName"|  
|SQLCMDDBNAME|-d|R|""|  
|SQLCMDLOGINTIMEOUT|-l|R/W|"8" (秒)|  
|SQLCMDSTATTIMEOUT|-t|R/W|"0" = 永遠等候|  
|SQLCMDHEADERS|-h|R/W|"0"|  
|SQLCMDCOLSEP|-s|R/W|" "|  
|SQLCMDCOLWIDTH|-w|R/W|"0"|  
|SQLCMDPACKETSIZE|-a|R|"4096"|  
|SQLCMDERRORLEVEL|-M|R/W|0|  
|SQLCMDMAXVARTYPEWIDTH|-y|R/W|"256"|  
|SQLCMDMAXFIXEDTYPEWIDTH|-y|R/W|"0" = 無限制|  
|SQLCMDEDITOR||R/W|"edit.com"|  
|SQLCMDINI||R|""|  
  
 SQLCMDUSER、SQLCMDPASSWORD 和 SQLCMDSERVER 會在使用 **:Connect**  
  
 時設定。  
  
 R 表示在程式初始化期間只能設定該值一次。  
  
 R/W 表示可以使用 **setvar** 命令修改該值，且後續的命令會受到新值的影響。  
  
## <a name="sqlcmd-commands"></a>sqlcmd 命令  
 除了 [!INCLUDE[tsql](../includes/tsql-md.md)] 內的 `sqlcmd` 陳述式之外，您也可以使用下列命令：  
  
|||  
|-|-|  
|**GO** [*計數*]|**：清單**|  
|[**:**] **RESET**|**：錯誤**|  
|[**:**] **ED**|**： Out**|  
|[**:**] **!!**|**:P erftrace**|  
|[**:**] **QUIT**|**： Connect**|  
|[**:**] **EXIT**|**：發生錯誤時**|  
|**： r**|**：說明**|  
|**： ServerList**|**： XML** [**ON** &#124; **OFF**]|  
|**： Setvar**|**： Listvar**|  
  
 使用 `sqlcmd` 命令時請注意下列事項：  
  
-   除了 GO 之外的所有 `sqlcmd` 命令開頭都必須加上冒號 (:)。  
  
    > [!IMPORTANT]  
    >  為了顧及與現有 **osql** 指令碼的回溯相容性，也會辨識部分沒有冒號的命令。 [**:**] 表示這一點。  
  
-   
  `sqlcmd` 命令必須在行首，才能夠辨識。  
  
-   所有 `sqlcmd` 命令都不區分大小寫。  
  
-   每個命令都必須在不同行中。 命令後面不能有 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式或另一個命令。  
  
-   命令會立即執行， 不會像 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式一樣放在執行緩衝區中。  
  
 **編輯命令**  
  [**:**] **ED**  
 啟動文字編輯器。 您可以利用這個編輯器編輯目前的 [!INCLUDE[tsql](../includes/tsql-md.md)] 批次，或上次執行的批次。 若要編輯上次執行的批次，在上一個批次執行完成之後，必須立即輸入 **ED** 命令。  
  
 文字編輯器由 SQLCMDEDITOR 環境變數來定義。 預設編輯器是 'Edit'。 若要變更編輯器，請設定 SQLCMDEDITOR 環境變數。 例如，若要將編輯器設為 [!INCLUDE[msCoName](../includes/msconame-md.md)] Notepad，請在命令提示字元之下，輸入：  
  
 `SET SQLCMDEDITOR=notepad`  
  
 [**:**] **RESET**  
 清除陳述式快取。  
  
 **：清單**  
 列印陳述式快取內容。  
  
 **變數**  
  **： Setvar** \< **var**> [ **"*`value`*"** ]  
 定義 `sqlcmd` 指令碼變數。 指令碼變數的格式如下： `$(VARNAME)`。  
  
 變數名稱不區分大小寫。  
  
 指令碼變數可以透過下列幾種方式設定：  
  
-   隱含地使用命令列選項。 例如， **-l**選項會設定 SQLCMDLOGINTIMEOUT `sqlcmd`變數。  
  
-   明確地利用 **:Setvar** 命令。  
  
-   在您執行 `sqlcmd` 之前，定義環境變數。  
  
> [!NOTE]  
>  
  `-X` 選項會讓您無法將環境變數傳給 `sqlcmd`。  
  
 如果使用 **:Setvar** 所定義的變數和環境變數同名，則以使用 **:Setvar** 所定義的變數優先。  
  
 變數名稱不能包含空格字元。  
  
 變數名稱的格式不能與變數運算式 (例如 $(var)) 相同。  
  
 如果指令碼變數的字串值包含空格，請用引號括住這個值。 如果未指定指令碼變數值，就會卸除指令碼變數。  
  
 **： Listvar**  
 顯示目前所設定之指令碼變數的清單。  
  
> [!NOTE]  
>  只會顯示由`sqlcmd`設定的腳本變數，以及使用 **： Setvar**命令所設定的腳本。  
  
 **輸出命令**  
  **：錯誤**   
 **_\<_**__ **檔案名_>|_ STDERR |STDOUT**    
 將所有錯誤輸出重新導向至 *filename*所指定的檔案、 **stderr** 或 **stdout**。 在指令碼中， **Error** 命令可以重複出現。 根據預設，錯誤輸出會傳送到 **stderr**。  
  
 *檔案名*  
 建立和開啟用來接收輸出的檔案。 如果檔案已經存在，它會截斷成零位元組。 如果因為權限或其他原因無法使用，就不會切換輸出，輸出會送往最後指定的目的地或預設目的地。  
  
 **STDERR**  
 將錯誤輸出切換到 **stderr** 資料流。 如果它已重新導向，資料流所重新導向的目標會接收這個錯誤輸出。  
  
 **輸出**  
 將錯誤輸出切換到 **stdout** 資料流。 如果它已重新導向，資料流所重新導向的目標會接收這個錯誤輸出。  
  
 **： Out \< ** __ **>** filename |  ** **STDERR| **STDOUT**  
 建立並將所有查詢結果重新導向至 *filename*所指定的檔案、 **stderr** 或 **stdout**。 根據預設，輸出會傳送到 **stdout**。 如果檔案已經存在，它會截斷成零位元組。 在指令碼中， **Out** 命令可以重複出現。  
  
 **:P erftrace \< ** __ **>** filename |  ** **STDERR| **STDOUT**  
 建立並將所有效能追蹤資訊重新導向至 *filename*所指定的檔案、 **stderr** 或 **stdout**。 根據預設，效能追蹤輸出會傳送到 **stdout**。 如果檔案已經存在，它會截斷成零位元組。 在指令碼中， **Perftrace** 命令可以重複出現。  
  
 **執行控制命令**  
  **：發生錯誤時**[ `exit`  |  `ignore`]  
 設定執行指令碼或批次發生錯誤時所要執行的動作。  
  
 使用 `exit` 選項時，`sqlcmd` 會結束作業，並會出現適當的錯誤值。  
  
 使用 `ignore` 選項時，`sqlcmd` 會忽略錯誤，並繼續執行批次或指令碼。 依預設，會列印一則錯誤訊息。  
  
 [**:**] **QUIT**  
 讓 `sqlcmd` 結束作業。  
  
 [**:**]**EXIT**[ **（*`statement`*）** ]  
 可讓您使用 SELECT 陳述式的結果做為 `sqlcmd` 的傳回值。 如果為數值，最後一個結果資料列的第一個資料行會轉換成 4 位元組的整數 (long)。 MS-DOS 會將低位元組傳給父處理序或作業系統錯誤層級。 Windows 200x 會傳遞完整的 4 位元組整數。 語法為：  
  
 `:EXIT(query)`  
  
 例如：  
  
 `:EXIT(SELECT @@ROWCOUNT)`  
  
 您也可以將 **EXIT** 參數併入批次檔中。 例如，在命令提示字元之下，輸入：  
  
 `sqlcmd -Q "EXIT(SELECT COUNT(*) FROM '%1')"`  
  
 `sqlcmd`公用程式會將括弧 **（）** 之間的所有內容傳送至伺服器。 如果系統預存程序選取某一組，傳回某個值，此時只會傳回選取的項目。 括號中沒有任何內容的 EXIT **()** 陳述式，會執行批次中在它前面的任何內容，然後結束作業，不傳回任何值。  
  
 指定不正確的查詢時，`sqlcmd` 會結束作業，不傳回任何值。  
  
 以下是 EXIT 格式清單：  
  
-   :EXIT  
  
 不執行批次，然後立即結束，不傳回任何值。  
  
-   :EXIT( )  
  
 執行批次之後，便結束作業，不傳回任何值。  
  
-   :EXIT(query)  
  
 執行包含查詢的批次，傳回查詢結果之後再結束。  
  
 如果在 `sqlcmd` 指令碼內使用 RAISERROR，且產生 127 狀態，`sqlcmd` 會結束作業，且會將訊息識別碼傳回用戶端。 例如：  
  
 `RAISERROR(50001, 10, 127)`  
  
 這個錯誤會使得 `sqlcmd` 指令碼結束作業，並將訊息識別碼 50001 傳回用戶端。  
  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會保留傳回值 -1 至 -99；`sqlcmd` 定義了下列其他傳回值：  
  
|傳回值|描述|  
|-------------------|-----------------|  
|-100|在選取傳回值之前發生錯誤。|  
|-101|在選取傳回值時，找不到任何資料列。|  
|-102|在選取傳回值時，發生轉換錯誤。|  
  
 **GO** [*計數*]  
 GO 會發出批次結束及執行任何快取的 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式的信號。 指定 *count*的值時，快取的陳述式將以單一批次執行 *count* 次。  
  
 **其他命令**  
  **： r \< ** _檔案名_**>**  
 將[!INCLUDE[tsql](../includes/tsql-md.md)] `sqlcmd` **指定<之檔案中的其他語句和命令，剖析至語句快取。 *`filename`* **  
  
 如果檔案包含的 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式後面沒有緊接著 **GO**，您必須在 **:r** 之後的一行輸入 **GO**。  
  
> [!NOTE]  
>  **\<**__ **>** 相對於執行所在`sqlcmd`的啟動目錄，會讀取 filename。  
  
 在發現批次結束字元之後，便會讀取和執行這個檔案。 您可以發出多個 **:r** 命令。 這個檔案可包含任何 `sqlcmd` 命令。 其中包括批次結束字元 **GO**。  
  
> [!NOTE]  
>  每次發現 **:r** 命令時，以互動模式顯示的行數便會加 1。 
  **:r** 命令會出現在 list 命令的輸出中。  
  
 **： Serverlist**  
 列出設定在本機的伺服器，以及在網路中進行廣播的伺服器名稱。  
  
 **： Connect** _server_name_[**\\**_instance_name_] [-l *timeout*] [-U *user_name* [-P *password*]]  
 連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體。 此外也會關閉目前的連接。  
  
 逾時選項：  
  
|||  
|-|-|  
|0|永久等候|  
|n>0|等候 n 秒|  
  
 SQLCMDSERVER 指令碼變數會反映目前作用中的連接。  
  
 如果沒有指定 *timeout* ，預設值就是 SQLCMDLOGINTIMEOUT 變數的值。  
  
 如果只指定 *user_name* (作為選項或作為環境變數)，則會提示使用者輸入密碼。 如果已設定 SQLCMDUSER 或 SQLCMDPASSWORD 環境變數，就不會提示。 如果既沒有提供選項，也沒有提供環境變數，就會利用 Windows 驗證模式來登入。 例如，若要利用整合式安全性連接 `instance1`( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]) 的執行個體 `myserver`，您將使用下列命令：  
  
 `:connect myserver\instance1`  
  
 若要利用指令碼變數來連接 `myserver` 的預設執行個體，您將使用下列命令：  
  
 `:setvar myusername test`  
  
 `:setvar myservername myserver`  
  
 `:connect $(myservername) $(myusername)`  
  
 [**:**]**!!**\< *命令*>  
 執行作業系統命令。 若要執行作業系統命令，請在行首輸入兩個驚歎號 (**!!**)，後面再接著作業系統命令。 例如：  
  
 `:!! Dir`  
  
> [!NOTE]  
>  這個命令會在執行 `sqlcmd` 的電腦上執行。  
  
 **： XML** [**ON** | **OFF**]  
 如需詳細資訊，請參閱本主題稍後的＜XML 輸出格式＞。  
  
 **：說明**  
 列出 `sqlcmd` 命令及各命令的簡短描述。  
  
### <a name="sqlcmd-file-names"></a>sqlcmd 檔案名稱  
 `sqlcmd`輸入檔可以使用 **-i**選項或 **： r**命令來指定。 輸出檔則可以使用 **-o** 選項或 **:Error**、 **:Out** 和 **:Perftrace** 命令予以指定。 以下列出使用這些檔案的幾項指導方針：  
  
-   **： Error**、 **： Out**和 **:P erftrace**應該使用不同** < *`filename`*** 的。 如果使用相同** < *`filename`* **的，來自命令的輸入可能會混合在一起。  
  
-   如果從本機電腦的 `sqlcmd` 呼叫位於遠端伺服器上的輸入檔，且檔案中包含磁碟機檔案路徑 (例如 :out c:\OutputFile.txt)， 便會在本機電腦建立輸出檔案，而不是在遠端伺服器建立。  
  
-   有效的檔案路徑包括： C\\**<*`filename`***： \\ \\ 、<\> \\ Server<共用 $ \\ ** < *`filename`* **>和「C:\Some\\**<*`file name`*** 資料夾」。 如果路徑中有空格，請使用引號。  
  
-   每個新的 `sqlcmd` 工作階段都會覆寫現有的同名檔案。  
  
### <a name="informational-messages"></a>參考用訊息  
 
  `sqlcmd` 會列印伺服器所傳送的所有參考用訊息。 在下列範例中，執行 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式之後，會列印一則參考用訊息。  
  
 在命令提示字元中，請輸入下列項目：  
  
 `sqlcmd`  
  
 `At the sqlcmd prompt type:`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 當您按 ENTER 時，會出現下列參考用訊息：「已將資料庫內容變更為 'AdventureWorks2012'」。  
  
### <a name="output-format-from-transact-sql-queries"></a>Transact-SQL 查詢的輸出格式  
 
  `sqlcmd` 會先列印包含選取清單中所指定之資料行名稱的資料行標頭。 資料行名稱是以 SQLCMDCOLSEP 字元分隔。 根據預設，這是一個空格。 如果資料行名稱長度小於資料行寬度，便會在輸出中填補空格直到下一個資料行。  
  
 這一行後面會接著一條由虛線字元組成的分隔線。 下列輸出顯示一個範例。  
  
 啟動 `sqlcmd`。 在 `sqlcmd` 命令提示字元處，請輸入下列項目：  
  
 `USE AdventureWorks2012;`  
  
 `SELECT TOP (2) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 當您按下 ENTER，就會傳回下列結果集。  
  
 `BusinessEntityID FirstName    LastName`  
  
 `---------------- ------------ ----------`  
  
 `285              Syed         Abbas`  
  
 `293              Catherine    Abel`  
  
 `(2 row(s) affected)`  
  
 雖然 `BusinessEntityID` 資料行的寬度只有 4 個字元，但它已擴充，能夠容納較長的資料行名稱。 依預設，輸出的長度最多為 80 個字元。 您可以利用 **-w** 選項或設定 SQLCMDCOLWIDTH 指令碼變數，變更此設定。  
  
### <a name="xml-output-format"></a>XML 輸出格式  
 FOR XML 子句所產生的 XML 輸出，會在連續資料流中以未格式化的形式輸出。  
  
 當您希望產生 XML 輸出時，請使用下列命令： `:XML ON`。  
  
> [!NOTE]  
>  
  `sqlcmd` 會以一般格式傳回錯誤訊息。 請注意，錯誤訊息也會以 XML 格式輸出至 XML 文字資料流。 如果使用 `:XML ON`，`sqlcmd` 就不會顯示參考用訊息。  
  
 若要將 XML 模式設定為關閉，請使用下列命令： `:XML OFF`。  
  
 在發出 XML OFF 命令之前，不應出現 GO 命令，因為 XML OFF 命令會將 `sqlcmd` 切換回資料列導向的輸出。  
  
 XML (資料流) 資料和資料列集不能混合。 如果在執行輸出 XML 資料流的 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式之前發出 XML ON 命令，輸出會混亂。 如果已發出 XML ON 命令，您就不能執行輸出正規資料列集的 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式。  
  
> [!NOTE]  
>  
  **:XML** 命令不支援 SET STATISTICS XML 陳述式。  
  
## <a name="sqlcmd-best-practices"></a>sqlcmd 最佳作法  
 請採用下列作法以提高安全性與效率。  
  
-   使用整合式安全性。  
  
-   在自動化環境中使用 `-X`。  
  
-   利用 NTFS 檔案系統權限保護輸入檔和輸出檔。  
  
-   為提高效能，請盡可能在單一 `sqlcmd` 工作階段中執行所有工作，而不要使用一連串的工作階段。  
  
-   將批次或查詢執行的逾時值，設定成高於您預期執行批次或查詢所需的時間值。  
  
## <a name="see-also"></a>另請參閱  
 [啟動 sqlcmd 公用程式](../relational-databases/scripting/sqlcmd-start-the-utility.md)   
 [使用 sqlcmd 執行 Transact-sql 腳本檔案](../relational-databases/scripting/sqlcmd-run-transact-sql-script-files.md)   
 [使用 sqlcmd 公用程式](../relational-databases/scripting/sqlcmd-use-the-utility.md)   
 [搭配腳本變數使用 sqlcmd](../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)   
 [使用 sqlcmd 連接到資料庫引擎](../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md)   
 [使用查詢編輯器編輯 SQLCMD 腳本](../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)   
 [管理作業步驟](../ssms/agent/manage-job-steps.md)   
 [建立 CmdExec 作業步驟](../ssms/agent/create-a-cmdexec-job-step.md)  
  
  
