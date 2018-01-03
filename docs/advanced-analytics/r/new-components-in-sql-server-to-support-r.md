---
title: "SQL Server 中的元件來支援 R |Microsoft 文件"
ms.custom: 
ms.date: 04/05/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 54e9ef3f-1136-471e-865a-7cf013673186
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2aa7a79610433c11270d146473f233747fda3d39
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="components-in-sql-server-to-support-r"></a>SQL Server 中支援 R 的元件

在 SQL Server 2016 和 2017年，database engine 包含選用元件的外部指令碼語言，包括 R，並將 Python 支援擴充性。 SQL Server 2016; 已加入的 R 語言支援SQL Server 2017 機器學習服務中已加入的 Python 支援。

本主題描述搭配 R 語言的新元件。 如需這些元件使用開放原始碼 R 的運作方式的討論，請參閱[R 互通性](r-interoperability-in-sql-server.md)

## <a name="components-and-providers"></a>元件和提供者

除了在架構概觀中所述的載入 R 語言並執行 R 程式碼的殼層之外，[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 也包含這些額外元件。

### <a name="launchpad"></a>Launchpad 

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]是所提供之服務[!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)]支援執行外部指令碼，類似於全文檢索索引和查詢服務，啟動處理全文檢索查詢的個別的主控件的方式。

Launchpad 服務只會啟動由 Microsoft 發行之信任的啟動器，或是經 Microsoft 認證符合效能和資源管理要求的啟動器。 這個名稱代表語言特有 launchers 相當直接：

  + R-rlauncher.dll 初始化
  + Python-PythonLauncher.dll

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服務在其自有的使用者帳戶下執行。 特定語言執行階段的每個附屬處理序會繼承 Launchpad 的使用者帳戶。 如需設定及啟動列的安全性內容的詳細資訊，請參閱[安全性概觀](../../advanced-analytics/r/security-overview-sql-server-r.md)。

### <a name="bxlserver-and-sql-satellite"></a>BxlServer 和 SQL 附屬項目

BxlServer 是管理之間的通訊的 Microsoft 所提供的可執行檔[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]R 執行階段和也實作 RevoScaleR 函式。 它會建立用來包含 R 工作階段的 Windows 工作物件、佈建每個 R 工作的安全工作資料夾，以及使用 SQL Satellite 管理 R 和 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 之間的資料傳輸。

實際上，BxlServer 附屬於 R，能與 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 搭配以支援 R 與 SQL Server 的整合。 BXL 代表二進位交換語言，並指的是用來移動資料有效 SQL Server 和外部處理序之間例如當您安裝 Microsoft R 用戶端或 Microsoft R Server 時，也會安裝 R BxlServer.dll 的資料格式。

SQL Satellite 是 SQL Server 2016 中新的擴充性 API，它是由資料庫引擎提供，以支援使用 C 或 C++ 實作的外部程式碼或外部執行階段。 BxlServer 使用 SQL Satellite 來和 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 通訊。

SQL Satellite 使用的自訂資料格式，已針對在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和外部指令碼語言之間快速傳輸資料最佳化。 它會在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和 R 之間通訊的期間，執行類型轉換並定義輸入和輸出資料集的結構描述。

BxlServer 將 SQL Satellite 用於下列工作：

  + 讀取輸入資料
  + 寫入輸出資料
  + 取得輸入引數
  + 寫入輸出引數
  + 錯誤處理
  + 寫入標準輸出和錯誤傳回給用戶端

可以使用擴充事件來監視 SQL Satellite。 如需詳細資訊，請參閱 [SQL Server R Services 的擴充事件](extended-events-for-sql-server-r-services.md)。

## <a name="communication-channels-between-components"></a>元件之間的通訊通道

+ **TCP/IP**

    根據預設，之間的內部通訊[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]和 SQL 附屬項目使用 TCP/IP。

+ **具名管道**

    BxlServer 之間的內部資料傳輸和[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]SQL 附屬透過使用專屬的壓縮資料格式來增強效能。 從 R 記憶體到 BxlServer 的資料會透過 BXL 格式的具名管線來交換。

+ **ODBC**

    外部資料科學用戶端之間的通訊和[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]執行個體使用 ODBC。 將 R 工作傳送到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 的帳戶必須具有連線到執行個體及執行外部指令碼的權限。 此外，該帳戶必須具有存取工作所使用任何資料的權限、寫入資料的權限 (例如，將結果儲存到資料表)，或建立資料庫物件的權限 (例如，將 R 函式儲存在新的預存程序之中)。

    當 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 用來做為遠端用戶端所傳送 R 工作的計算內容且該 R 命令必須從外部資源擷取資料時，會使用 ODBC 來回寫。 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 會將發出遠端 R 命令的使用者身分識別，對應到目前執行個體上的使用者身分識別，並使用該使用者的認證來執行 ODBC 命令。 執行此 ODBC 呼叫所需的連接字串可從用戶端程式碼取得。

    在指令碼中使用 **RODBC**，將可進行其他的 ODBC 呼叫。 針對存取關聯式資料庫中的資料，RODBC 是常用的 R 套件。不過，它的效能通常慢於 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 所使用的類似提供者。 許多 R 指令碼會使用 RODBC 的內嵌呼叫，以擷取「次要」資料集以供分析之用。 例如，定型模型的預存程序可能會定義 SQL 查詢，以取得用於定型模型的資料，但卻使用內嵌 RODBC 呼叫來取得其他因素、執行查詢，或是從文字檔或 Excel 等外部來源取得新資料。

    下列程式碼說明內嵌在 R 指令碼中的 RODBC 呼叫：

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **其他通訊協定**

    也可以使用適用於 「 區塊 」 或資料傳送至遠端用戶端可能需要的處理程序。XDF 格式支援的 Microsoft。 實際的資料傳輸是透過編碼的 blob。

## <a name="interaction-of-components"></a>元件的互動

先前描述的元件架構可確保開放原始碼的 R 程式碼能以「現狀」運作，同時大幅提高在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦上執行程式碼的效能。 依 R 程式碼啟動方式而異，元件與 R 執行階段和 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 資料庫引擎的互動機制略有不同。 本節將摘要說明重要的案例。

### <a name="r-scripts-executed-from-sql-server-in-database"></a>從 SQL Server 中的資料庫中執行 R 指令碼

從 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]「內部」執行的 R 程式碼會透過呼叫預存程序來執行。 因此，任何可以進行預存程序呼叫的應用程式都能初始化 R 程式碼的執行。  之後，[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 會如下圖摘要說明的方式來管理 R 程式碼的執行。

![rsql_indb780-01](media/script_in-db-r.png)

1. 對於 R 執行階段的要求會以傳遞到預存程序 ([sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)) 的參數 _@language='R'_ 表示。 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 將此要求傳送到 Launchpad 服務。
2. Launchpad 服務會啟動適當的啟動器，在此案例中為 RLauncher。
3. RLauncher 啟動外部 R 處理序。
4. BxlServer 會與 R 執行階段合作，以管理與 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 的資料交換，以及處理結果的儲存。
5. SQL 附屬管理相關工作的通訊並處理具有[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。
6. BxlServer 使用 SQL Satellite 來與 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 進行狀態和結果的通訊。
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 會取得結果，並關閉相關工作和處理序。

### <a name="r-scripts-executed-from-a-remote-client"></a>從遠端用戶端執行的 R 指令碼

當從支援 Microsoft R 遠端資料科學用戶端連線，您可以執行 R 函數的內容中[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]使用 RevoScaleR 函式。 這和先前的工作流程不同，下圖會摘要說明。

![rsql_fromR2db-01](media/remote-sqlcc-from-r2.png)

1. RevoScaleR 函數 R 執行階段會呼叫連結的函式會依序呼叫 BxlServer。
2. BxlServer 會隨 Microsoft R 提供，且與 R 執行階段在分開的處理序中執行。
3. BxlServer 會判斷連線目標並使用 ODBC 初始化連線，並在 R 資料來源物件中將認證做為連接字串的一部分來傳遞。
4. BxlServer 開啟對 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體的連線。
5. R 的呼叫，[啟動列] 會叫用服務，這會開啟啟動適當啟動器 RLauncher。 之後，R 程式碼的處理方式就類似從 T-SQL 執行 R 程式碼的處理方式。
6. RLauncher 呼叫安裝在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦上 R 執行階段的執行個體。
7. 結果會傳回 BxlServer。
8. SQL Satellite 管理與 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 的通訊，並清理相關的工作物件。
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 將結果傳遞回用戶端。

## <a name="next-steps"></a>後續步驟

[架構概觀](architecture-overview-sql-server-r.md)

[安全性概觀](security-overview-sql-server-r.md)

[安全性考量](security-considerations-for-the-r-runtime-in-sql-server.md)
