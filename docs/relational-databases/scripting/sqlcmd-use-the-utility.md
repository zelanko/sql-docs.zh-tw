---
title: "使用 sqlcmd 公用程式 | Microsoft Docs"
ms.custom: 
ms.date: 06/06/2017
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- Transact-SQL statements, executing
- command prompt utilities [SQL Server], sqlcmd
- statements [SQL Server], executing
- sqlcmd utility, about sqlcmd utility
ms.assetid: 3ec89119-7314-43ef-9e91-12e72bb63d62
caps.latest.revision: "50"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 0969b3f39f94ec3832cc762ec9419425e099000f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sqlcmd---use-the-utility"></a>sqlcmd - 使用公用程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] **sqlcmd** 公用程式是命令列公用程式，可用來執行特定的互動式 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式和指令碼，以及用於自動化 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼工作。 若要以互動方式使用 **sqlcmd** ，或是要建立透過 **sqlcmd**執行的指令碼檔案，使用者必須了解 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 一般而言， **sqlcmd** 公用程式的使用方式如下：  
  
-   使用者可以像是在命令提示字元中工作一般，輸入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 結果會顯示在命令提示字元視窗中。 若要開啟命令提示字元視窗，請在 [Windows 搜尋] 方塊中輸入 "cmd"，並按一下 [命令提示字元] 來開啟。 在命令提示字元中，輸入 **sqlcmd** ，後面接著您要使用的一串選項。 如需 **sqlcmd**所支援選項的完整清單，請參閱 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)。  
  
-   使用者可指定要執行的單一 **陳述式，或者將公用程式指向包含要執行之** 陳述式的文字檔，來提交 [!INCLUDE[tsql](../../includes/tsql-md.md)] sqlcmd [!INCLUDE[tsql](../../includes/tsql-md.md)] 工作。 輸出通常會導向文字檔，不過，也可以在命令提示字元上顯示。  
  
-   [查詢編輯器中的](../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md) SQLCMD 模式 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
-   SQL Server 管理物件 (SMO)  
  
-   SQL Server Agent CmdExec 作業  
  
## <a name="typically-used-sqlcmd-options"></a>一般使用的 sqlcmd 選項  
  
-   伺服器選項 (**-S**) 識別 **sqlcmd** 所連接的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
-   驗證選項 (**-E**、**-U** 和 **-P**) 指定供 **sqlcmd** 用來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的認證。 **注意：****-E** 選項是預設值，不需要予以指定。  
  
-   輸入選項 (**-Q**、**-q** 和 **-i**) 識別 **sqlcmd** 的輸入位置。  
  
-   輸出選項 (**-o**) 指定 **sqlcmd** 存放其輸出的檔案。  
  
## <a name="connect-to-the-sqlcmd-utility"></a>連接到 sqlcmd 公用程式  
  
-   使用 Windows 驗證連接到預設執行個體，以互動方式執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    sqlcmd -S <ComputerName>  
    ```  
  
    > **注意：** 上述範例未指定 **-E** ，因為它是預設值，而且 **sqlcmd** 會使用 Windows 驗證連接到預設的執行個體。  
  
-   使用 Windows 驗證連接到具名執行個體，以互動方式執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    sqlcmd -S <ComputerName>\<InstanceName>  
    ```  
  
     或  
  
    ```  
    sqlcmd -S .\<InstanceName>  
    ```  
  
-   使用 Windows 驗證，並且指定輸入和輸出檔案，以連接到具名執行個體：  
  
    ```  
    sqlcmd -S <ComputerName>\<InstanceName> -i <MyScript.sql> -o <MyOutput.rpt>  
    ```  
  
-   使用 Windows 驗證連接到本機電腦上的預設執行個體、執行查詢，並在查詢完成後讓 **sqlcmd** 繼續執行：  
  
    ```  
    sqlcmd -q "SELECT * FROM AdventureWorks2012.Person.Person"  
    ```  
  
-   使用 Windows 驗證連接到本機電腦上的預設執行個體、執行查詢、將輸出導向至檔案，然後在查詢完成後結束 **sqlcmd** ：  
  
    ```  
    sqlcmd -Q "SELECT * FROM AdventureWorks2012.Person.Person" -o MyOutput.txt  
    ```  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接到具名執行個體，以互動方式執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式 ( **sqlcmd** 會提示您輸入密碼)：  
  
    ```  
    sqlcmd -U MyLogin -S <ComputerName>\<InstanceName>  
    ```  
  
    > **提示！！** 若要查看 **sqlcmd** 公用程式所支援的選項清單，請執行： `sqlcmd -?`。  
  
## <a name="run-transact-sql-statements-interactively-by-using-sqlcmd"></a>使用 sqlcmd 以互動方式執行 Transact-SQL 陳述式  
 您可以使用 **sqlcmd** 公用程式，以互動方式在 [命令提示字元] 視窗中執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 若要使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] sqlcmd **以互動方式執行**陳述式，請執行公用程式，但是不要使用 **-Q**、 **-q**、 **-Z**或 **-i** 選項指定任何輸入檔或查詢。 例如：  
  
 `sqlcmd -S <ComputerName>\<InstanceName>`  
  
 如果在沒有輸入檔或查詢的情況下執行命令， **sqlcmd** 會連接到指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，然後顯示新的一行，其中在 `1>` 後面跟著的閃爍底線，即稱為 **sqlcmd** 提示字元。 `1` 表示此處是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的第一行，而 **sqlcmd** 提示字元則是您開始輸入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的位置。  
  
 在 **sqlcmd** 提示字元中，您可以輸入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式及 **sqlcmd** 命令 (例如 **GO** 及 **EXIT**)。 每個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式會放在稱為陳述式快取的緩衝區中。 這些陳述式會在您輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 命令並按 ENTER 後，傳送至 **GO** 。 若要結束 **sqlcmd**，在新的一行的開頭輸入 **EXIT** 或 **QUIT** 。  
  
 若要清除陳述式快取，請輸入 **:RESET**。 輸入 **^C** 會導致 **sqlcmd** 結束。 在發出**^C** 命令後，也可以使用 **^C** 來停止執行陳述式快取。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式可藉由輸入 **:ED** 命令及 **sqlcmd** 提示字元。 此時會開啟編輯器，而在編輯過 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式並關閉編輯器之後，修訂的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式即顯示於命令視窗。 請輸入 **GO** 執行修訂的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
## <a name="quoted-strings"></a>使用引號的字串  
 系統會直接使用引號括住的字元，而不做額外處理，但是連續輸入兩個引號以將引號插入字串中的情況除外。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將這個字元順序視為一個引號 (不過，翻譯動作是在伺服器內進行)。指令碼變數出現於字串時，並不會展開。  
  
 例如：  
  
 `sqlcmd`  
  
 `PRINT "Length: 5"" 7'";`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Length: 5" 7'`  
  
## <a name="strings-that-span-multiple-lines"></a>跨越多行的字串  
 **sqlcmd** 支援其字串跨越多行的指令碼。 例如，下列 `SELECT` 陳述式雖然跨越多行，但是當您輸入 `GO`後按下 ENTER 鍵時，所執行的只是單一的字串。  
  
 `SELECT First line`  
  
 `FROM Second line`  
  
 `WHERE Third line;`  
  
 `GO`  
  
## <a name="interactive-sqlcmd-example"></a>互動的 sqlcmd 範例  
 這是您以互動方式執行 **sqlcmd** 時所看到的範例。  
  
 當您開啟 [命令提示字元] 視窗時，只會出現類似下面這一行：  
  
 `C:\> _`  
  
 這表示資料夾 `C:\` 是目前的資料夾，如果您指定了檔案名稱，則 Windows 將會在該資料夾中尋找這個檔案。  
  
 輸入 **sqlcmd** ，連接到本機電腦的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設執行個體，[命令提示字元] 視窗的內容如下：  
  
 `C:\>sqlcmd`  
  
 `1> _`  
  
 這表示您已經連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，而且 `sqlcmd` 已經準備好要接受 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式與 `sqlcmd` 命令。 在 `1>` 後面的閃爍底線是 `sqlcmd` 提示字元，該字元標示將顯示您輸入之陳述式與命令的位置。 現在請輸入 **USE AdventureWorks2012** 並按下 ENTER，然後輸入 **GO** ，再按下 ENTER。 [命令提示字元] 視窗的內容將如下所示：  
  
 `sqlcmd`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Changed database context to 'AdventureWorks2012'.`  
  
 `1> _`  
  
 輸入 `USE AdventureWorks2012` 之後按下 ENTER，會指示 `sqlcmd` 開始新的一行。 輸入 `GO,` 之後按下 ENTER，會指示 `sqlcmd` 將 `USE AdventureWorks2012` 陳述式傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。 `sqlcmd` 便接著傳回訊息指出 `USE` 陳述式已順利完成，並且顯示新的 `1>` 提示字元，表示可以再輸入新的陳述式或命令。  
  
 下列範例顯示當您輸入 `SELECT` 陳述式、再輸入 `GO` 執行 `SELECT`，然後輸入 `EXIT` 結束 `sqlcmd`時，[命令提示字元] 視窗中出現的內容：  
  
 `sqlcmd`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `SELECT TOP (3) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `BusinessEntityID   FirstName                 LastName`  
  
 `----------- -------------------------------- -----------`  
  
 `1           Syed                             Abbas`  
  
 `2           Catherine                        Abel`  
  
 `3           Kim                              Abercrombie`  
  
 `(3 rows affected)`  
  
 `1> EXIT`  
  
 `C:\>`  
  
 在 `3> GO` 這一行後面的那幾行，是 `SELECT` 陳述式的輸出。 產生輸出後， `sqlcmd` 會重設 `sqlcmd` 提示字元，並顯示 `1>`。 在 `EXIT` 行輸入 `1>`之後，[命令提示字元] 視窗會顯示和您初次開啟這個視窗時同樣的一行。 這表示 `sqlcmd` 已經結束其工作階段。 您現在可以輸入另一個 `EXIT` 命令，來關閉 [命令提示字元] 視窗。  
  
## <a name="running-transact-sql-script-files-using-sqlcmd"></a>使用 sqlcmd 執行 Transact-SQL 指令碼檔案  
 您可以使用 **sqlcmd** 來執行資料庫指令碼檔案。 指令碼檔案是文字檔，其中混合了 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式、 **sqlcmd** 命令及指令碼變數。 如需如何編寫指令碼變數的詳細資訊，請參閱 [以指令碼變數使用 sqlcmd](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)。 **sqlcmd** 在指令碼檔案中使用陳述式、命令及指令碼變數的方式，與它使用互動方式輸入陳述式及命令的方式類似。 主要的差別在於 **sqlcmd** 會讀取整個輸入檔而不暫停，而不是等待使用者輸入陳述式、命令及指令碼變數。  
  
 建立資料庫指令碼檔案有許多不同的方式：  
  
-   您可以互動方式在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中建立一組 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]陳述式並進行偵錯，然後將 [查詢] 視窗的內容儲存為指令碼檔案。  
  
-   您可以使用文字編輯器 (如「記事本」)，來建立包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的文字檔。  
  
## <a name="examples"></a>範例  
  
### <a name="a-running-a-script-by-using-sqlcmd"></a>A. 使用 sqlcmd 執行指令碼  
 啟動「記事本」，然後輸入下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `SELECT TOP (3) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 建立名為 `MyFolder` 的資料夾，然後在資料夾 `MyScript.sql` 中將指令碼儲存為檔案 `C:\MyFolder`。 在命令提示字元中輸入下列命令，以執行指令碼並將輸出存放在 `MyOutput.txt` 的 `MyFolder`中：  
  
 `sqlcmd -i C:\MyFolder\MyScript.sql -o C:\MyFolder\MyOutput.txt`  
  
 當您在「記事本」中檢視 `MyOutput.txt` 的內容時，會看到下列項目：  
  
 `Changed database context to 'AdventureWorks2012'.`  
  
 `BusinessEntityID FirstName   LastName`  
  
 `---------------- ----------- -----------`  
  
 `1                Syed        Abbas`  
  
 `2                Catherine   Abel`  
  
 `3                Kim         Abercrombie`  
  
 `(3 rows affected)`  
  
### <a name="b-using-sqlcmd-with-a-dedicated-administrative-connection"></a>B. 透過專用管理連接使用 sqlcmd  
 在下列範例中，使用 `sqlcmd` 透過專用管理員連接 (DAC) 連接到發生封鎖問題的伺服器。  
  
 `C:\>sqlcmd -S ServerName -A`  
  
 `1> SELECT blocked FROM sys.dm_exec_requests WHERE blocked <> 0;`  
  
 `2> GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `spid   blocked`  
  
 `------ -------`  
  
 `62       64`  
  
 `(1 rows affected)`  
  
 使用 `sqlcmd` 結束封鎖處理序。  
  
 `1> KILL 64;`  
  
 `2> GO`  
  
### <a name="c-using-sqlcmd-to-execute-a-stored-procedure"></a>C. 使用 sqlcmd 執行預存程序  
 下列範例顯示如何使用 `sqlcmd`來執行預存程序。 建立下列預存程序。  
  
 `USE AdventureWorks2012;`  
  
 `IF OBJECT_ID ( ' dbo.ContactEmailAddress, 'P' ) IS NOT NULL`  
  
 `DROP PROCEDURE dbo.ContactEmailAddress;`  
  
 `GO`  
  
 `CREATE PROCEDURE dbo.ContactEmailAddress`  
  
 `(`  
  
 `@FirstName nvarchar(50)`  
  
 `,@LastName nvarchar(50)`  
  
 `)`  
  
 `AS`  
  
 `SET NOCOUNT ON`  
  
 `SELECT EmailAddress`  
  
 `FROM Person.Person`  
  
 `WHERE FirstName = @FirstName`  
  
 `AND LastName = @LastName;`  
  
 `SET NOCOUNT OFF`  
  
 在 `sqlcmd` 提示字元中，輸入下列命令：  
  
 `C:\sqlcmd`  
  
 `1> :Setvar FirstName Gustavo`  
  
 `1> :Setvar LastName Achong`  
  
 `1> EXEC dbo.ContactEmailAddress $(Gustavo),$(Achong)`  
  
 `2> GO`  
  
 `EmailAddress`  
  
 `-----------------------------`  
  
 `gustavo0@adventure-works.com`  
  
### <a name="d-using-sqlcmd-for-database-maintenance"></a>D. 使用 sqlcmd 進行資料庫維護  
 下列範例顯示如何使用 `sqlcmd` 進行資料庫維護工作。 以下列程式碼建立 `C:\BackupTemplate.sql` 。  
  
 `USE master;`  
  
 `BACKUP DATABASE [$(db)] TO DISK='$(bakfile)';`  
  
 在 `sqlcmd` 提示字元中，輸入下列命令：  
  
 `C:\ >sqlcmd`  
  
 `1> :connect <server>`  
  
 `Sqlcmd: Successfully connected to server <server>.`  
  
 `1> :setvar db msdb`  
  
 `1> :setvar bakfile c:\msdb.bak`  
  
 `1> :r c:\BackupTemplate.sql`  
  
 `2> GO`  
  
 `Changed database context to 'master'.`  
  
 `Processed 688 pages for database 'msdb', file 'MSDBData' on file 2.`  
  
 `Processed 5 pages for database 'msdb', file 'MSDBLog' on file 2.`  
  
 `BACKUP DATABASE successfully processed 693 pages in 0.725 seconds (7.830 MB/sec)`  
  
### <a name="e-using-sqlcmd-to-execute-code-on-multiple-instances"></a>E. 使用 sqlcmd 在多個執行個體上執行程式碼  
 下列在檔案中的程式碼會顯示連接到兩個執行個體的指令碼。 請注意， `GO` 是在連接第二個執行個體之前出現。  
  
 `:CONNECT <server>\,<instance1>`  
  
 `EXEC dbo.SomeProcedure`  
  
 `GO`  
  
 `:CONNECT <server>\,<instance2>`  
  
 `EXEC dbo.SomeProcedure`  
  
 `GO`  
  
### <a name="e-returning-xml-output"></a>E. 傳回 XML 輸出  
 下列範例顯示 XML 輸出如何在連續資料流中傳回未格式化的資料。  
  
 `C:\>sqlcmd -d AdventureWorks2012`  
  
 `1> :XML ON`  
  
 `1> SELECT TOP 3 FirstName + ' ' + LastName + ', '`  
  
 `2> FROM Person.Person`  
  
 `3> GO`  
  
 `Syed Abbas, Catherine Abel, Kim Abercrombie,`  
  
### <a name="f-using-sqlcmd-in-a-windows-script-file"></a>F. 在 Windows 指令碼檔案中使用 sqlcmd  
 **sqlcmd**命令 (例如 `sqlcmd -i C:\InputFile.txt -o C:\OutputFile.txt,` ) 可以在 .bat 檔案中與 VBScript 一起執行。 在這種情況下，請不要使用互動式選項。 **sqlcmd** 必須安裝在執行 .bat 檔案的電腦上。  
  
 首先，建立下列四個檔案：  
  
-   C:\badscript.sql  
  
    ```  
    SELECT batch_1_this_is_an_error  
    GO  
    SELECT 'batch #2'  
    GO  
    ```  
  
-   C:\goodscript.sql  
  
    ```  
    SELECT 'batch #1'  
    GO  
    SELECT 'batch #2'  
    GO  
    ```  
  
-   C:\returnvalue.sql  
  
    ```  
    :exit(select 100)  
    @echo off  
    C:\windowsscript.bat  
    @echo off  
  
    echo Running badscript.sql  
    sqlcmd -i badscript.sql -b -o out.log  
    if not errorlevel 1 goto next1  
    echo == An error occurred   
  
    :next1  
  
    echo Running goodscript.sql  
    sqlcmd -i goodscript.sql -b -o out.log  
    if not errorlevel 1 goto next2  
    echo == An error occurred   
  
    :next2  
    echo Running returnvalue.sql  
    sqlcmd -i returnvalue.sql -o out.log  
    echo SQLCMD returned %errorlevel% to the command shell  
  
    :exit  
    ```  
  
-   C:\windowsscript.bat  
  
    ```  
    @echo off  
  
    echo Running badscript.sql  
    sqlcmd -i badscript.sql -b -o out.log  
    if not errorlevel 1 goto next1  
    echo == An error occurred   
  
    :next1  
  
    echo Running goodscript.sql  
    sqlcmd -i goodscript.sql -b -o out.log  
    if not errorlevel 1 goto next2  
    echo == An error occurred   
  
    :next2  
    echo Running returnvalue.sql  
    sqlcmd -i returnvalue.sql -o out.log  
    echo SQLCMD returned %errorlevel% to the command shell  
  
    :exit  
    ```  
  
 然後，在命令提示字元執行 `C:\windowsscript.bat`：  
  
 `C:\>windowsscript.bat`  
  
 `Running badscript.sql`  
  
 `== An error occurred`  
  
 `Running goodscript.sql`  
  
 `Running returnvalue.sql`  
  
 `SQLCMD returned 100 to the command shell`  
  
### <a name="g-using-sqlcmd-to-set-encryption-on-windows-azure-sql-database"></a>G. 使用 sqlcmd 設定 Windows Azure SQL 資料庫的加密  
 **sqlcmd**可以在與 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 資料的連接上執行，以指定加密及憑證信任。 有兩個 **sqlcmd**`` 選項可以使用：  
  
-   -N 參數是由用戶端用來要求加密的連接。 這個選項相當於 ADO.net 選項 `ENCRYPT = true`。  
  
-   –C 參數是由用戶端所設定，以隱含方式信任伺服器憑證而且不進行驗證。 這個選項相當於 ADO.net 選項 `TRUSTSERVERCERTIFICATE = true`。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服務不支援 SQL Server 執行個體上的所有可用 `SET` 選項。 當對應的 `SET` 選項設定為 `ON` 或 `OFF`時，下列選項會擲回錯誤：  
  
-   SET ANSI_DEFAULTS  
  
-   SET ANSI_NULLS  
  
-   SET REMOTE_PROC_TRANSACTIONS  
  
-   SET ANSI_NULL_DEFAULT  
  
 以下 SET 選項不會擲回例外狀況，但不能使用。 這些選項已被取代：  
  
-   SET CONCAT_NULL_YIELDS_NULL  
  
-   SET ANSI_PADDING  
  
-   SET QUERY_GOVERNOR_COST_LIMIT  
  
#### <a name="syntax"></a>語法  
 下列範例會參考 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 提供者設定的案例，包括： `ForceProtocolEncryption = False`、 `Trust Server Certificate = No`  
  
 使用 Windows 認證來連接，並加密通訊：  
  
```  
SQLCMD –E –N  
  
```  
  
 使用 Windows 認證及信任伺服器憑證進行連接：  
  
```  
SQLCMD –E –C  
  
```  
  
 使用 Windows 認證進行連接、加密通訊並信任伺服器憑證：  
  
```  
SQLCMD –E –N –C  
  
```  
  
 下列範例會參考 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 提供者設定的案例，包括： `ForceProtocolEncryption = True`、 `TrustServerCertificate = Yes`。  
  
 使用 Windows 認證進行連接、加密通訊並信任伺服器憑證：  
  
```  
SQLCMD –E  
  
```  
  
 使用 Windows 認證進行連接、加密通訊並信任伺服器憑證：  
  
```  
SQLCMD –E –N  
  
```  
  
 使用 Windows 認證進行連接、加密通訊並信任伺服器憑證：  
  
```  
SQLCMD –E –T  
  
```  
  
 使用 Windows 認證進行連接、加密通訊並信任伺服器憑證：  
  
```  
SQLCMD –E –N –C  
  
```  
  
 如果提供者指定 `ForceProtocolEncryption = True` ，則會啟用加密，即使 `Encrypt=No` 在連接字串中。  
  
## <a name="more-about-sqlcmd"></a>深入了解 sqlcmd  
 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)   
 [以指令碼變數使用 sqlcmd](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)   
 [使用查詢編輯器編輯 SQLCMD 指令碼](../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)   
 [管理作業步驟](http://msdn.microsoft.com/library/51352afc-a0a4-428b-8985-f9e58bb57c31)   
 [建立 CmdExec 作業步驟](http://msdn.microsoft.com/library/b48da5b4-6fe7-4eb7-bade-dc7d697c6d5c)  
  
  
