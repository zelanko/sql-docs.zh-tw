---
title: 在 SQL Server Machine Learning 服務的擴充性架構 |Microsoft Docs
description: 外部程式碼支援的 SQL Server database engine，使用的雙重架構關聯式資料上執行 R 和 Python 指令碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: fae8beb4f865c537f00fa8b58a01cafe09541d71
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43892865"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>在 SQL Server Machine Learning 服務的擴充性架構 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 已在伺服器上執行外部指令碼，例如 R 或 Python 擴充性架構。 做為核心資料庫引擎的擴充，語言執行階段環境中執行指令碼。 

## <a name="background"></a>背景

若要支援 R 執行階段的 SQL Server 2016 中引進了擴充性架構。 SQL Server 2017 新增了適用於 Python 的支援

擴充性架構的目的是要提供 SQL Server 與資料科學語言，例如 R 和 Python，公開開發期間的移動到生產階段前和保護資料的資料科學解決方案時降低阻力之間的介面程序。 藉由執行受信任的指令碼語言，在受 SQL Server 的安全架構，資料庫管理員可以維護安全性，同時讓資料科學家企業資料的存取權。

下圖以視覺化方式描述機會和可延伸架構的優勢。

  ![使用 SQL Server 的整合目標](../media/ml-service-value-add.png "機器學習服務增加價值")

呼叫預存程序，也可以執行任何 R 或 Python 指令碼，並傳回結果做為表格式結果直接為 SQL Server，輕鬆地產生或取用任何可以傳送 SQL 查詢和處理結果的應用程式的機器學習服務。

+ 外部指令碼執行受限於 SQL Server 資料安全性，一位使用者執行外部指令碼可以在這裡同樣可在 SQL 查詢中存取資料。 如果查詢失敗，因為沒有足夠的權限，在相同的使用者執行的指令碼也會在基於相同原因失敗。 SQL Server 安全性是在資料表、 資料庫和執行個體層級強制執行。 資料庫系統管理員可以管理使用者存取、 外部指令碼，所使用的資源新增至伺服器的外部程式碼程式庫。  

+ 調整與最佳化的機會有雙重基礎： 透過資料庫平台提升 (資料行存放區索引[資源控管](../../advanced-analytics/r/resource-governance-for-r-services.md))，和適用於 R 和 Python 的 Microsoft 程式庫是用來進行資料的延伸模組特定提升科學模型。 R 是單一執行緒，而 RevoScaleR 函數是多執行緒、 能夠將工作負載散發到多個核心。

+ 部署使用 SQL Server 的方法： 包裝外部指令碼 預存程序的情況下，內嵌 SQL 或 T-SQL 查詢呼叫的函式，例如傳回從預測模型的結果保存在伺服器上的預測。

+ 使用 R 和 Python 開發人員建立的特定工具和 Ide 技能可以這些工具中撰寫程式碼，然後程式碼移植到 SQL Server。

## <a name="architecture-diagram"></a>架構圖

這個架構的設計使得在不同的處理序中從 SQL Server，但在內部管理資料和 SQL Server 上的作業要求的鏈結的元件執行的外部指令碼。 根據 SQL Server 版本，支援的語言擴充功能包括 R 和 Python。 

  ![元件架構](../media/generic-architecture.png "元件架構")

元件包括**Launchpad**用來叫用特定語言的啟動器 （R 或 Python） 的語言和程式庫特有的邏輯，來載入解譯器和程式庫的服務。 啟動器會載入語言執行平台，再加上任何專屬的模組。 例如，如果您的程式碼包含 RevoScaleR 函式，會載入 RevoScaleR 解譯器。 **BxlServer**並**SQL Satellite**管理與 SQL Server 的通訊和資料傳輸。

## <a name="launchpad"></a>Launchpad

SQL Server 受信任的 Launchpad 是一項服務，負責管理和執行外部指令碼，類似於全文檢索索引及查詢服務啟動個別的主機，來處理全文檢索查詢的方式。 Launchpad 服務可以開始只信任的啟動器，由 Microsoft 發行或，都經過 Microsoft 為符合需求的效能與資源管理。

| 受信任的啟動器 | 延伸模組 | SQL Server 版本 |
|-------------------|-----------|---------------------|
| 針對 R 語言的 rlauncher.dll 初始化 | [R 擴充功能](extension-r.md) | SQL Server 2016，SQL Server 2017 |
| 適用於 Python 3.5 Pythonlauncher.dll | [Python 擴充功能](extension-python.md) | SQL Server 2017 |

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服務在其自有的使用者帳戶下執行。 如果您變更執行 Launchpad 的帳戶，請務必這樣做時使用 SQL Server 組態管理員，以確保變更會寫入相關檔案。

若要在特定的支援語言中執行工作，[啟動列] 從集區，取得受保護的背景工作帳戶，並啟動附屬處理序來管理外部執行階段。 每個附屬處理序會繼承 Launchpad 的使用者帳戶，並執行指令碼的持續期間使用該背景工作帳戶。 如果指令碼會使用平行處理序，它們會建立相同且單一背景工作帳戶。

## <a name="bxlserver-and-sql-satellite"></a>BxlServer 和 SQL Satellite

**BxlServer**是管理 SQL Server 和 Python 或 r 之間通訊的 Microsoft 所提供的可執行檔它會建立 Windows 作業物件會用來包含外部指令碼工作階段，為每個外部指令碼工作中，佈建安全工作資料夾，並使用 SQL Satellite 來管理外部執行階段和 SQL Server 之間的資料傳輸。 如果您執行[Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx)執行作業時，您可能會看到 BxlServer 的一個或多個執行個體。

實際上，BxlServer 是附隨於執行階段環境，適用於 SQL Server 來傳輸資料和管理工作的語言。 BXL 代表 「 二進位交換語言，而是指用來有效率地移動資料，SQL Server 和外部處理序之間的資料格式。 BxlServer 還有相關的產品，例如 Microsoft R Client 和 Microsoft R Server 中很重要的一部分。

**SQL Satellite**是資料庫引擎啟動 SQL Server 2016，支援外部程式碼中包含的擴充性 API 或使用 C 或 c + + 實作的外部執行階段。

BxlServer 將 SQL Satellite 用於下列工作：

+ 讀取輸入資料
+ 寫入輸出資料
+ 取得輸入引數
+ 寫入輸出引數
+ 錯誤處理
+ 將 STDOUT 和 STDERR 寫回用戶端

SQL Satellite 使用最適合的自訂資料格式的 SQL Server 和外部指令碼語言之間快速的資料傳輸。 它會執行類型轉換，並在 SQL Server 和外部指令碼執行階段之間的通訊期間，定義輸入和輸出資料集的結構描述。

使用擴充事件 (xEvents) 的 windows，可以監視 SQL Satellite。 如需詳細資訊，請參閱 <<c0> [ 適用於 R 的擴充事件](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)並[適用於 Python 的擴充事件](../../advanced-analytics/python/extended-events-for-python.md)。

## <a name="communication-channels-between-components"></a>元件之間的通訊通道

元件和資料平台之間的通訊協定是以這一節所述。

+ **TCP/IP**

  根據預設，SQL Server 和 SQL Satellite 的內部通訊會使用 TCP/IP。

+ **具名管道**

  BxlServer 和 SQL Server 透過 SQL Satellite 之間的內部資料傳輸會使用專屬的壓縮資料格式，來增強效能。 使用具名管道的 BXL 格式語言執行時間與 BxlServer 之間交換資料。

+ **ODBC**

  外部資料科學用戶端與遠端的 SQL Server 執行個體之間的通訊會使用 ODBC。 指令碼會將工作傳送到 SQL Server 的帳戶必須具有這兩個權限，才能連接到執行個體，以及執行外部指令碼。

  此外，根據工作中，帳戶可能會需要這些權限：

  + 讀取作業所使用的資料
  + 將資料寫入至資料表： 例如，當儲存結果儲存至資料表
  + 建立資料庫物件： 例如，如果將外部指令碼儲存為新的預存程序的一部分。

  當 SQL Server 作為計算內容中執行的指令碼遠端用戶端，並可執行檔必須從外部來源擷取資料、 回寫會使用 ODBC。 SQL Server 對應至目前的執行個體上的使用者身分識別發出遠端命令的使用者身分識別，並執行 ODBC 命令使用該使用者的認證。 執行此 ODBC 呼叫所需的連接字串可從用戶端程式碼取得。

+ **RODBC (只有 R)** 

  在指令碼中使用 **RODBC**，將可進行其他的 ODBC 呼叫。 RODBC 是常用的 R 套件，用來存取關聯式資料庫; 中的資料不過，它的效能低於一般 SQL Server 所使用的類似提供者。 許多 R 指令碼會使用 RODBC 的內嵌呼叫，以擷取「次要」資料集以供分析之用。 例如，定型模型的預存程序可能會定義 SQL 查詢，以取得用於定型模型的資料，但卻使用內嵌 RODBC 呼叫來取得其他因素、執行查詢，或是從文字檔或 Excel 等外部來源取得新資料。

  下列程式碼說明內嵌在 R 指令碼中的 RODBC 呼叫：

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **其他通訊協定**

  使用 「 區塊 」，或將資料傳輸回遠端用戶端可能需要的處理程序也可以使用[XDF 檔案格式](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)。 實際的資料傳輸是透過已編碼的 blob。

## <a name="see-also"></a>另請參閱

+ [SQL Server 中的 R 延伸模組](extension-r.md)
+ [SQL Server 中的 Python 擴充功能](extension-python.md)