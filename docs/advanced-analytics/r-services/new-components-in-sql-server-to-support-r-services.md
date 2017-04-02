---
title: "在 SQL Server 支援 R 服務中的新元件 | Microsoft Docs"
ms.custom: ""
ms.date: "06/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 54e9ef3f-1136-471e-865a-7cf013673186
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# 在 SQL Server 支援 R 服務中的新元件

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 包含所提供的新元件 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 資料庫引擎支援的 R 語言的擴充性。 這些元件的安全性由 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和稍後會討論在詳細資料。

## 新的 SQL Server 元件和提供者

除了載入 R 和架構概觀中所述執行 R 程式碼的殼層 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 包含下列額外的元件。

### **啟動列** 
   [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 是所提供的新服務 [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)] 支援外部指令碼，類似於全文檢索索引和查詢服務啟動個別的主控件處理全文檢索查詢的方式執行。 
  
  Launchpad 服務會啟動只信任啟動程式，Microsoft 所發行的或，都經過 Microsoft 以符合需求的效能和資源管理。 在 [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)], ，R 是目前唯一的外部所支援的語言 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]。
  
   [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服務會在它自己的使用者帳戶下執行。 每個附屬程序，為特定語言執行階段將會繼承的啟動列的使用者帳戶。 如需設定及啟動列的安全性內容的詳細資訊，請參閱 [安全性概觀](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)。

### **BxlServer 和 SQL 衛星**
  BxlServer 是管理之間的通訊的 Microsoft 所提供的可執行檔 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] R 執行階段和也會實作 ScaleR 函式。 它會建立 Windows 作業物件，用來包含 R 工作階段，每個 R 工作，提供安全工作資料夾，並使用 SQL 附屬管理 R 之間的資料傳輸和 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。  

  實際上，BxlServer 是適用於 R [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 支援的 R 與 SQL Server 的整合。 BXL 代表二進位 Exchange 語言，而是指用來與 SQL Server 外部的程序，例如 r 有效率地移動資料的資料格式 

 SQL 附屬是新的擴充性 API 由外部程式碼或使用 C 或 c + + 實作的外部執行階段支援的資料庫引擎的 SQL Server 2016 中。 R 目前唯一支援的執行階段。 BxlServer 的通訊使用 SQL 附屬 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。
 
  使用最快速的資料傳輸之間的自訂的資料格式，SQL 附屬 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和外部指令碼語言。 它會執行類型轉換，並定義輸入和輸出資料集的結構描述之間的通訊期間 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和鍵。

  BxlServer 使用 SQL 附屬來執行這些工作︰ 
  - 讀取輸入的資料
  - 寫入輸出資料
  - 取得輸入引數
  - 寫入輸出引數
  - 錯誤處理
  - 寫入 STDOUT 和 STDERR 回覆給用戶端

  SQL 附屬受到使用擴充的事件。 如需詳細資訊，請參閱 [擴充的事件，適用於 SQL Server R Services](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)。


## 元件之間的通訊通道

+ **TCP/IP** 根據預設，之間的內部通訊 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和 SQL 附屬使用 TCP/IP。

+ **具名管道**

  BxlServer 之間的內部資料傳輸和 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 透過 SQL 附屬使用專屬的壓縮資料格式來提升效能。 從 R 記憶體 BxlServer 來交換資料時透過 BXL 格式的具名管道。 
  
+ **ODBC** 外部資料科學的用戶端之間的通訊和 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用 ODBC 的執行個體。 傳送 R 帳戶工作至 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 必須有兩個連接的執行個體，以及執行外部指令碼的權限。 此外，帳戶必須具有存取工作，是用來寫入資料 （例如，如果將結果儲存至資料表），或是建立資料庫物件 （例如，如果儲存的 R 函式做為新的預存程序的一部分） 的任何資料的權限。

  當 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 是從遠端用戶端傳送的 R 工作的計算內容和 R 命令必須從外部來源擷取資料，ODBC 會使用回寫。 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 將遠端 R 命令發出至目前的執行個體上的使用者身分識別的使用者身分識別對應，並執行 ODBC 命令使用該使用者的認證。 執行這個 ODBC 呼叫所需的連接字串是從用戶端程式碼中取得。
  
  其他的 ODBC 呼叫可在指令碼中使用 **RODBC**。 RODBC 是受歡迎的 R 封裝，用來存取關聯式資料庫中的資料不過，它的效能會比可比較的提供者所使用的速度較慢 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 許多的 R 指令碼會使用內嵌的呼叫 RODBC 這種擷取 「 次要 」 資料集，以供分析。 比方說，定型模型的預存程序可能會定義 SQL 查詢，以取得的資料培訓模型，但使用內嵌的 RODBC 呼叫，以取得其他因素，來執行查詢，或取得新的資料從外部來源，例如文字檔案或 Excel。

  下列程式碼將說明在 R 指令碼中內嵌的 RODBC 呼叫︰
   ~~~~
  library(RODBC);
  connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
  dbhandle <- odbcDriverConnect(connStr)
  OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
  ~~~~

+ **其他通訊協定** 可能需要在 「 區塊 」 工作或資料傳送至遠端用戶端的程序也可以使用。Microsoft r 實際的資料傳輸所支援的 XDF 格式是透過編碼的 blob。

## 元件的互動

前面所述的元件架構已經提供保證 「 開放原始碼 R 程式碼可以運作，而提供大幅增加執行的程式碼的效能 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦。 R 執行階段使用的元件如何互動的機制和 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 資料庫引擎和不同稍微根據 R 程式碼啟動的方式。 本節將摘要列出重要案例。 
 
### 從 SQL Server （資料庫） 執行的 R 指令碼

R 程式碼執行的 「 內部 」 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 呼叫預存程序來執行。 因此，任何應用程式都可以進行呼叫的預存程序可以起始 R 程式碼的執行。  此後 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 管理的 R 程式碼執行，在下圖將摘要說明。

![rsql_indb780-01](../../advanced-analytics/r-services/media/rsql-indb780-01.png)

1. R 執行階段的要求會以參數 _@language = 'R'_ 傳遞至預存程序， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Launchpad 服務來傳送此要求。
2. Launchpad 服務啟動適當的啟動器。在此情況下，RLauncher。
3. RLauncher 啟動外部 R 程序。
4. R 執行階段管理的資料交換的 BxlServer 座標 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和儲存體的工作結果。
5. 從頭到尾，SQL 附屬管理相關工作的相關通訊，並使用處理 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。
6. BxlServer 會使用 SQL 附屬溝通狀態，並造成 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 取得結果，並關閉相關的工作和程序。 


### 從遠端用戶端執行 R 指令碼

從支援 Microsoft R 的遠端資料科學用戶端連接時，您可以執行的 R 函式的內容中 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用 ScaleR 函式。 這是從上一個不同的工作流程，並在下圖摘要說明。


![rsql_fromR2db-01](../../advanced-analytics/r-services/media/rsql-fromr2db-01.png)

1. 對於 ScaleR 函式，R 執行階段會呼叫連結的函式會呼叫 BxlServer。 
2. BxlServer 會隨附於 Microsoft R，並從 R 執行階段執行不同的處理序。
3. BxlServer 決定連線目標，並啟始連線使用 ODBC，傳遞做為 R 資料來源物件中的連接字串的一部分提供的認證。
4. BxlServer 開啟的連接 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體。
5. 對於 R 呼叫時，叫用服務時，[啟動列] 是開啟啟動適當的啟動器 RLauncher。 之後，處理 R 程式碼則從 T-SQL 執行 R 程式碼的程序類似。
6. RLauncher 會呼叫執行個體上已安裝的 R 執行階段 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦。 
7. BxlServer 會傳回結果。
8. SQL 附屬管理之間的通訊 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和相關的工作物件的清除。
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 結果傳回給用戶端。

## 另請參閱
[架構概觀](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)
