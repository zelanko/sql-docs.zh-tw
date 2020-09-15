---
title: 擴充性架構
description: 本文描述用來在 SQL 伺服器機器學習服務上執行外部 Python 或 R 指令碼的擴充性架構結構。 指令碼會在語言執行階段環境中執行，作為核心資料庫引擎的延伸模組。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2303fdda5ae28fb9a384a174a128b2487e637f7e
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173310"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>SQL Server 機器學習服務的擴充性結構 
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

本文描述用來在 SQL 伺服器機器學習服務上執行外部 Python 或 R 指令碼的擴充性架構結構。 指令碼會在語言執行階段環境中執行，作為核心資料庫引擎的延伸模組。

## <a name="background"></a>背景

擴充性架構是在 SQL Server 2016 中引進，以透過 [R Services](../r/sql-server-r-services.md) 支援 R 執行階段。 SQL Server 2017 和更新版本則透過[機器學習服務](../sql-server-machine-learning-services.md)支援 Python。

擴充性架構的目的是要在 SQL Server 和資料科學語言 (例如 R 和 Python) 之間提供介面。 目標是要減少將資料科學解決方案移到生產環境時的摩擦，並保護在開發程序中公開的資料。 藉由在受 SQL Server 管理的安全架構中執行信任的指令碼語言，資料庫管理員可以維護安全性，同時允許資料科學家存取企業資料。

下列圖表以視覺化方式描述可擴充結構的機會和優點。

  ![與 SQL Server 整合的目標](../media/ml-service-value-add.png "機器學習服務加入的價值")

您可以藉由呼叫預存程序來執行外部指令碼，而結果會以表格式結果直接傳回 SQL Server。 這可讓您輕鬆地從任何可傳送 SQL 查詢並處理結果的應用程式產生或取用機器學習。

+ 外部指令碼執行受限於 SQL Server 資料安全性。 執行外部指令碼的使用者只能存取在 SQL 查詢中同樣可用的資料。 如果查詢因為權限不足而失敗，則由相同使用者執行的指令碼也會因為相同的原因而失敗。 SQL Server 安全性會在資料表、資料庫和執行個體層級強制執行。 資料庫管理員可以管理使用者存取、外部腳本所使用的資源，以及加入至伺服器的外部程式碼程式庫。  

+ 調整和最佳化機會有雙重基礎：透過資料庫平台 (資料行存放區索引、[資源治理](../../machine-learning/administration/resource-governor.md)) 取得；和延伸模組特定的取得，例如，將適用於 R 和 Python 的 Microsoft 程式庫用於資料科學模型時。 雖然 R 是單一執行緒的，但 RevoScaleR 函式是多執行緒的，能夠將工作負載分散到多個核心。

+ 使用 SQL Server 方法的部署。 這些可能是包裝外部指令碼的預存程序、內嵌 SQL 或 T-SQL 查詢，呼叫函式 (例如 PREDICT) 來從保存在伺服器上的預測模型傳回結果。

+ 在特定工具和 IDE 中具有熟練技能的開發人員可以在這些工具中撰寫程式碼，然後將程式碼移植到 SQL Server。

## <a name="architecture-diagram"></a>架構圖

此架構的設計，是為了讓外部指令碼在 SQL Server 的個別處理序中執行，而不是在 SQL Server 上於內部管理資料和作業要求鏈的元件中執行。 取決於 SQL Server 的版本，支援的語言延伸模組包括 [R](extension-r.md)、[Python](extension-python.md) 和協力廠商語言，例如 Java 和 .NET。

  ***Windows 中的元件架構：***
  
  ![Windows 元件架構](../media/generic-architecture-windows.png "元件架構")
  
  ***Linux 中的元件架構：***

  ![Linux 元件架構](../media/generic-architecture-linux.png "元件架構")
  
元件包含**啟動控制板**服務，用來叫用外部執行階段和程式庫特定邏輯，以載入解譯器和程式庫。 啟動器會載入語言執行階段，以及任何專屬模組。 例如，如果您的程式碼包含 RevoScaleR 函式，就會載入 RevoScaleR 解譯器。 **BxlServer** 和 **SQL Satellite** 管理對 SQL Server 的通訊和資料傳輸。 

在 Linux 中，SQL 會使用**啟動控制板**服務來與每個使用者的不同啟動控制板程序通訊。

<a name="launchpad"></a>

## <a name="launchpad"></a>Launchpad

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 是新服務，可管理和執行外部指令碼，就如同全文索引及查詢服務啟動個別的主機來處理全文查詢。 啟動控制板服務只會啟動由 Microsoft 發行之信任的啟動器，或是經 Microsoft 認證符合效能和資源管理要求的啟動器。

| 信任的啟動器 | 分機 | SQL Server 版本 |
|-------------------|-----------|---------------------|
| Windows 版 R 語言的 RLauncher.dll | [R 延伸模組](extension-r.md) | SQL Server 2016 及更新版本 |
| Windows 版 Python 3.5 的 Pythonlauncher.dll | [Python 延伸模組](extension-python.md) | SQL Server 2017 和更新版本 |
| Linux 版 R 語言的 RLauncher.so | [R 延伸模組](extension-r.md) | SQL Server 2019 和更新版本 |
| Linux 版 Python 3.5 的 Pythonlauncher.so | [Python 延伸模組](extension-python.md) | SQL Server 2019 和更新版本 |

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服務在其自有的使用者帳戶下執行。 如果您變更執行啟動控制板的帳戶，請務必使用 SQL Server 組態管理員來變更，以確保變更會寫入相關檔案中。

在 Windows 中，系統會針對您已新增 SQL Server 機器學習服務的每個資料庫引擎執行個體，建立個別的 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服務。 每個資料庫引擎執行個體都有一個啟動控制板服務，因此如果您有多個支援外部指令碼的執行個體，就會每個都有一個啟動控制板服務。 資料庫引擎執行個體會繫結至為它建立的啟動控制板。 預存程序或 T-SQL 中的所有外部指令碼叫用，都會導致 SQL Server 服務呼叫為相同執行個體建立的啟動控制板服務。

若要以特定受支援的語言執行工作，啟動控制板會從集區取得安全的背景工作帳戶，並啟動附屬處理序來管理外部執行階段。 每個附屬處理序都會繼承啟動控制板的使用者帳戶，並在指令碼執行期間使用該背景工作帳戶。 如果指令碼使用平行處理序，則會以相同的單一背景工作帳戶建立它們。

在 Linux 中，只支援一個資料庫引擎執行個體，而且有一個繫結至該執行個體的啟動控制板服務。 當執行指令碼時，啟動控制板服務會以低權限使用者帳戶 (**mssql_satellite**) 啟動一個個別的啟動控制板處理序。 每個附屬處理序都繼承啟動控制板的 mssql_satellite 使用者帳戶，並在指令碼執行期間使用該帳戶。

## <a name="bxlserver-and-sql-satellite"></a>BxlServer 和 SQL Satellite

**BxlServer** 是 Microsoft 提供的可執行檔，可以管理 SQL Server 和語言執行階段之間的通訊。 它會針對 Windows 建立用於包含外部指令碼工作階段的工作物件 (或針對 Linux 建立命名空間)。 它也會為每個外部指令碼作業佈建安全工作資料夾，並使用 SQL Satellite 來管理外部執行階段和 SQL Server 之間的資料傳輸。 如果您在作業執行時執行[處理序總管](https://technet.microsoft.com/sysinternals/processexplorer.aspx)，您可能會看到一或多個 BxlServer 執行個體。

事實上，BxlServer 是一種語言執行階段環境的隨附項目，可以搭配 SQL Server 來傳輸資料及管理工作。 BXL 代表「二進位交換語言」(Binary Exchange Language)，是指用來在 SQL Server 和外部處理序之間有效率地移動資料的資料格式。 BxlServer 也是 Microsoft R Client 和 Microsoft R Server 等相關產品的重要部分。

**SQL Satellite** 是資料庫引擎中的擴充性 API，它支援使用 C 或 C++ 實作的外部程式碼或外部執行階段。

BxlServer 將 SQL Satellite 用於下列工作：

+ 讀取輸入資料
+ 寫入輸出資料
+ 取得輸入引數
+ 寫入輸出引數
+ 錯誤處理
+ 將 STDOUT 和 STDERR 寫回用戶端

SQL Satellite 使用的自訂資料格式，已針對在 SQL Server 和外部指令碼語言之間快速傳輸資料最佳化。 它會在 SQL Server 和外部指令碼執行階段之間通訊的期間，執行型別轉換並定義輸入和輸出資料集的結構描述。

您可以使用 Windows 擴充事件 (xEvents) 來監視 SQL Satellite。 如需詳細資訊，請參閱 [SQL Server 機器學習服務的擴充事件](../../machine-learning/administration/extended-events.md)。

## <a name="communication-channels-between-components"></a>元件之間的通訊通道

本節描述元件和資料平台之間的通訊協定。

+ **TCP/IP**

  根據預設，SQL Server 和 SQL Satellite 之間的內部通訊是使用 TCP/IP。

+ **具名管道**

  BxlServer 和 SQL Server 之間透過 SQL Satellite 的內部資料傳輸，會使用專屬的壓縮資料格式來加強效能。 資料在語言執行階段和 BxlServer 之間，是使用具名管道以 BXL 格式交換。

+ **ODBC**

  外部資料科學用戶端和遠端 SQL Server 執行個體之間的通訊是使用 ODBC。 將指令碼工作傳送到 SQL Server 的帳戶必須有連線到執行個體及執行外部指令碼的權限。

  此外，取決於工作，帳戶可能需要下列權限：

  + 讀取由作業使用的資料
  + 將資料寫入至資料表：例如，將結果儲存至資料表時
  + 建立資料庫物件：例如，如果將外部指令碼儲存為新預存程序的一部分。

  當 SQL Server 作為從遠端用戶端執行指令碼的計算內容，且可執行檔必須從外部來源取得資料時，ODBC 會用於回寫。 SQL Server 會將發出遠端命令的使用者身分識別，對應到目前執行個體上的使用者身分識別，並使用該使用者的認證來執行 ODBC 命令。 執行此 ODBC 呼叫所需的連接字串可從用戶端程式碼取得。

+ **RODBC (僅限 R)** 

  在指令碼中使用 **RODBC**，將可進行其他的 ODBC 呼叫。 針對存取關聯式資料庫中的資料，RODBC 是常用的 R 套件。不過，它的效能通常慢於 SQL Server 所使用的類似提供者。 許多 R 指令碼會使用 RODBC 的內嵌呼叫，以擷取「次要」資料集以供分析之用。 例如，定型模型的預存程序可能會定義 SQL 查詢，以取得用於定型模型的資料，但卻使用內嵌 RODBC 呼叫來取得其他因素、執行查詢，或是從文字檔或 Excel 等外部來源取得新資料。

  下列程式碼說明內嵌在 R 指令碼中的 RODBC 呼叫：

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **其他通訊協定**

  可能需要以「區塊」運作或將資料傳輸回遠端用戶端的處理序也可以使用 [XDF 檔案格式](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf) \(英文\)。 實際的資料傳輸是透過已編碼的 Blob 來進行。

## <a name="see-also"></a>另請參閱

+ [SQL Server 中的 R 延伸模組](extension-r.md)
+ [SQL Server 中的 Python 延伸模組](extension-python.md)