---
title: R 語言和 Python 腳本的擴充性架構
description: SQL Server 資料庫引擎的外部程式碼支援, 具有在關聯式資料上執行 R 和 Python 腳本的雙重架構。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 4ee27fd68563be336f5bc98bb5b51b200f1dff71
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345128"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning 服務中的擴充性架構 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 具有可在伺服器上執行外部腳本 (例如 R 或 Python) 的擴充性架構。 腳本會在語言執行時間環境中執行, 做為核心資料庫引擎的延伸。 

## <a name="background"></a>背景

擴充性架構是在 SQL Server 2016 中引進, 以支援 R 執行時間。 SQL Server 2017 新增對 Python 的支援

擴充性架構的目的是要在 SQL Server 和資料科學語言 (例如 R 和 Python) 之間提供介面, 以減少將資料科學解決方案移到生產環境時的摩擦, 並保護在開發期間公開的資料。流程. 藉由在 SQL Server 管理的安全架構中執行信任的指令碼語言, 資料庫管理員可以維護安全性, 同時允許資料科學家存取企業資料。

下圖以視覺化方式描述可延伸架構的機會和優點。

  ![與 SQL Server 整合的目標](../media/ml-service-value-add.png "Machine Learning 服務值新增")

任何 R 或 Python 腳本都可以藉由呼叫預存程式來執行, 而結果會以表格式結果直接傳回 SQL Server, 讓您可以輕鬆地從任何可傳送 SQL 查詢並處理結果的應用程式產生或取用機器學習。

+ 外部腳本的執行受限於 SQL Server 資料安全性, 而執行外部腳本的使用者只能存取在 SQL 查詢中同樣可用的資料。 如果查詢因為許可權不足而失敗, 則相同使用者執行的腳本也會因為相同的原因而失敗。 SQL Server 安全性會在資料表、資料庫和實例層級強制執行。 資料庫管理員可以管理使用者存取、外部腳本所使用的資源, 以及加入至伺服器的外部程式碼程式庫。  

+ 調整和優化機會具有雙重基礎: 當適用于 R 和 Python 的 Microsoft 程式庫用於資料科學模型時, 可透過資料庫平臺 (資料行存放區索引、[資源管理](../../advanced-analytics/r/resource-governance-for-r-services.md)) 和延伸模組特定增益來取得。 雖然 R 是單一執行緒的, 但 RevoScaleR 函式是多執行緒的, 能夠將工作負載分散到多個核心。

+ 部署使用 SQL Server 方法: 包裝外部腳本、內嵌 SQL 或 T-SQL 查詢的預存程式, 其會呼叫函數 (例如 PREDICT), 以從保存在伺服器上的預測模型傳回結果。

+ 在特定工具和 Ide 中, 具備既定技能的 R 和 Python 開發人員可以在這些工具中撰寫程式碼, 然後將程式碼移植到 SQL Server。

## <a name="architecture-diagram"></a>架構圖

此架構的設計, 是為了讓外部腳本在 SQL Server 的個別進程中執行, 而不是在內部管理 SQL Server 的資料和作業要求鏈的元件。 視 SQL Server 版本而定, 支援的語言擴充功能包括 R 和 Python。 

  ![元件架構](../media/generic-architecture.png "元件架構")

元件包含一個  啟動列服務, 用來叫用語言特定的啟動器 (R 或 Python)、語言和程式庫特定邏輯以載入解譯器和程式庫。 啟動器會載入語言執行時間, 加上任何專屬模組。 例如, 如果您的程式碼包含 RevoScaleR 函數, 就會載入 RevoScaleR 解譯器。 **BxlServer**和**SQL 衛星**會使用 SQL Server 來管理通訊和資料傳輸。

<a name="launchpad"></a>

## <a name="launchpad"></a>Launchpad

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]是管理和執行外部腳本的服務, 類似于全文檢索索引和查詢服務啟動個別主控制項來處理全文檢索查詢的方式。 啟動列服務只能啟動由 Microsoft 發佈的信任啟動器, 或已由 Microsoft 認證, 以符合效能和資源管理的需求。

| 信任的啟動器 | 延伸模組 | SQL Server 版本 |
|-------------------|-----------|---------------------|
| R 語言的 RLauncher | [R 擴充功能](extension-r.md) | SQL Server 2016, SQL Server 2017 |
| 適用于 Python 3.5 的 Pythonlauncher | [Python 延伸模組](extension-python.md) | SQL Server 2017 |

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服務在其自有的使用者帳戶下執行。 如果您變更執行啟動列的帳戶, 請務必使用 SQL Server 組態管理員, 以確保變更會寫入相關的檔案中。

系統會[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]針對您已加入 SQL Server Machine Learning 服務的每個資料庫引擎實例, 建立個別的服務。 每個資料庫引擎實例都有一個啟動列服務, 因此如果您有多個具有外部腳本支援的實例, 就會有一個啟動列服務。 資料庫引擎實例會系結至為其建立的啟動列服務。 在預存程式或 T-sql 中, 所有外部腳本的調用都會導致 SQL Server 服務呼叫針對相同實例所建立的啟動列服務。

若要以特定支援的語言執行工作, 啟動列會從集區取得安全的工作者帳戶, 並開始附屬進程來管理外部執行時間。 每個附屬進程都會繼承啟動列的使用者帳戶, 並在腳本執行期間使用該背景工作帳戶。 如果腳本使用平行處理常式, 則會以相同的單一背景工作帳戶來建立它們。

## <a name="bxlserver-and-sql-satellite"></a>BxlServer 和 SQL 附屬

**BxlServer**是由 Microsoft 提供的可執行檔, 負責管理 SQL Server 與 Python 或 R 之間的通訊。它會建立用來包含外部腳本會話的 Windows 工作物件、為每個外部腳本作業布建安全的工作資料夾, 並使用 SQL 附屬來管理外部執行時間和 SQL Server 之間的資料傳輸。 如果您在作業執行時執行[Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx) , 您可能會看到一個或多個 BxlServer 實例。

實際上, BxlServer 是一種語言執行時間環境的隨附, 可以搭配 SQL Server 來傳輸資料及管理工作。 BXL 代表二進位交換語言, 而是指用來在 SQL Server 和外部進程之間有效率地移動資料的資料格式。 BxlServer 也是相關產品 (例如 Microsoft R Client 和 Microsoft R Server) 的重要部分。

**SQL 附屬**項是包含在資料庫引擎中的擴充性 API (從 SQL Server 2016 開始), 其支援使用 C 或C++所執行的外部程式碼或外部執行時間。

BxlServer 將 SQL Satellite 用於下列工作：

+ 讀取輸入資料
+ 寫入輸出資料
+ 取得輸入引數
+ 寫入輸出引數
+ 錯誤處理
+ 將 STDOUT 和 STDERR 寫回用戶端

SQL 衛星使用的自訂資料格式已針對 SQL Server 與外部指令碼語言之間的快速資料傳輸優化。 它會執行類型轉換, 並在 SQL Server 和外部腳本執行時間之間的通訊期間, 定義輸入和輸出資料集的架構。

您可以使用 windows 擴充的事件 (xEvents) 來監視 SQL 附屬項。 如需詳細資訊, 請參閱適用于[R 的擴充事件](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)和[Python 的擴充事件](../../advanced-analytics/python/extended-events-for-python.md)。

## <a name="communication-channels-between-components"></a>元件之間的通道

本節將說明元件和資料平臺之間的通訊協定。

+ **TCP/IP**

  根據預設, SQL Server 和 SQL 附屬之間的內部通訊會使用 TCP/IP。

+ **具名管道**

  透過 SQL 附屬 BxlServer 和 SQL Server 之間的內部資料傳輸, 會使用專屬的壓縮資料格式來增強效能。 使用具名管道, 在語言執行時間與 BxlServer 的 BXL 格式之間交換資料。

+ **ODBC**

  外部資料科學用戶端和遠端 SQL Server 實例之間的通訊會使用 ODBC。 將腳本工作傳送至 SQL Server 的帳戶必須具有連接到實例和執行外部腳本的兩個許可權。

  此外, 視工作而定, 帳戶可能需要下列許可權:

  + 讀取作業所使用的資料
  + 將資料寫入資料表: 例如, 將結果儲存至資料表時
  + 建立資料庫物件: 例如, 如果在新的預存程式中儲存外部腳本, 則為。

  當 SQL Server 做為從遠端用戶端執行之腳本的計算內容, 且可執行檔必須從外部來源取得資料時, ODBC 會用於回寫。 SQL Server 會將發出遠端命令之使用者的身分識別對應至目前實例上使用者的識別, 並使用該使用者的認證來執行 ODBC 命令。 執行此 ODBC 呼叫所需的連接字串可從用戶端程式碼取得。

+ **RODBC (僅限 R)** 

  在指令碼中使用 **RODBC**，將可進行其他的 ODBC 呼叫。 RODBC 是常用的 R 封裝, 用來存取關係資料庫中的資料。不過, 其效能通常會比 SQL Server 所使用的可比較提供者慢。 許多 R 指令碼會使用 RODBC 的內嵌呼叫，以擷取「次要」資料集以供分析之用。 例如，定型模型的預存程序可能會定義 SQL 查詢，以取得用於定型模型的資料，但卻使用內嵌 RODBC 呼叫來取得其他因素、執行查詢，或是從文字檔或 Excel 等外部來源取得新資料。

  下列程式碼說明內嵌在 R 指令碼中的 RODBC 呼叫：

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **其他通訊協定**

  可能需要處理「區塊」或將資料傳輸回遠端用戶端的程式, 也可以使用[XDF 檔案格式](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)。 實際的資料傳輸是透過編碼的 blob。

## <a name="see-also"></a>另請參閱

+ [SQL Server 中的 R 擴充功能](extension-r.md)
+ [SQL Server 中的 Python 延伸模組](extension-python.md)