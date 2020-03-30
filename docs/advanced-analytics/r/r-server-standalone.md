---
title: 什麼是獨立 Machine Learning Server 或 R 伺服器？
description: SQL Server 設定中的獨立 R 伺服器和 Machine Learning Server 簡介
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/13/2019
ms.topic: overview
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 2412bfb8bcd3cacc2db2702879353b92e328b09a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727391"
---
# <a name="what-are-standalone-machine-learning-server-or-r-server-in-sql-server"></a>什麼是 SQL Server 中的獨立 Machine Learning Server 或 R 伺服器？
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 提供獨立於 SQL Server 執行的獨立 R 伺服器或 Machine Learning Server 的安裝支援。 根據您的 SQL Server 版本而定，獨立伺服器具有開放原始碼 R (可能也有 Python) 的基礎，並與 Microsoft 中的高效能程式庫重疊，以大規模新增統計和預測性分析。 程式庫也會啟用以 R 或 Python 編寫指令碼的機器學習工作。 

在 SQL Server 2016 中，這項功能稱為 **R Server (獨立式)** ，且僅限於 R。 在 SQL Server 2017 中，它稱為 **Machine Learning Server (獨立式)** ，且包括 R 和 Python。  

> [!Note]
> 如同 SQL Server 安裝程式所安裝，獨立伺服器的功能相當於非 SQL 品牌版本的 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)，支援相同的使用者案例，包括遠端執行、運作化和 Web 服務，以及 R 和 Python 程式庫的完整集合。

## <a name="components"></a>元件

SQL Server 2016 僅限 R。 SQL Server 2017 支援 R 和 Python。 下表描述每個版本的功能。

| 元件 | 描述 |
|-----------|-------------|
| R 套件 | [**RevoScaleR**](ref-r-revoscaler.md) 是可調整 R 的主要程式庫，其中包含資料操作、轉換、視覺效果和分析的功能。  <br/>[**MicrosoftML**](ref-r-microsoftml.md) 新增機器學習演算法來建立自訂模型，以進行文字分析、影像分析及情感分析。 <br/>[**sqlRUtils**](ref-r-sqlrutils.md) 提供協助程式函式，可將 R 指令碼放入 T-SQL 預存程序、向資料庫註冊預存程序，以及從 R 開發環境執行預存程序。<br/>[**mrsdeploy**](operationalization-with-mrsdeploy.md) 提供 Web 服務部署 (僅限 SQL Server 2017)。 <br/>[**olapR**](ref-r-olapr.md) 是用來在 R 中指定 MDX 查詢。|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open) 是 Microsoft 的 R 開放原始碼散發。包含套件和解譯器。 請一律使用安裝程式中配套的 MRO 版本。 |
| R 工具 | R 主控台視窗和命令提示字元是 R 散發套件中的標準工具。 在 \Program files\Microsoft SQL Server\140\R_SERVER\bin\x64 尋找。 |
| R 範例和指令碼 |  開放原始碼 R 和 RevoScaleR 套件包含內建的資料集，讓您可以使用預先安裝的資料來建立和執行指令碼。 在 \Program files\Microsoft SQL Server\140\R_SERVER\library\datasets and \library\RevoScaleR 尋找。 |
| Python 套件 | [**revoscalepy**](../python/ref-py-revoscalepy.md) 是可擴充 Python 的主要程式庫，其中包含用於資料操作、轉換、視覺效果和分析的功能。 <br/>[**microsoftml**](../python/ref-py-microsoftml.md) 新增機器學習演算法來建立自訂模型，以進行文字分析、影像分析及情感分析。  |
| Python 工具 | 內建的 Python 命令列工具適用於臨機操作測試和工作。 在 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\python.exe 尋找工具。 |
| Anaconda | Anaconda 是 Python 和基本套件的開放原始碼散發套件。 |
| Python 範例和指令碼 | 像 R 一樣，Python 包含內建的資料集和指令碼。 在 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data 尋找 revoscalepy 資料。 |
| R 和 Python 中的預先定型模型 | 預先定型的模型是針對特定使用案例所建立，並由 Microsoft 的資料科學工程團隊進行維護。 您可以使用您所提供的新資料輸入，依實際情況使用預先定型的模型來對文字中的正負面情感進行評分，或偵測影像中的特徵。 獨立伺服器支援預先定型的模型且可以使用，但是您無法透過 SQL Server 安裝程式來安裝。 如需詳細資訊，請參閱[在 SQL Server上安裝預先定型機器學習模型](../install/sql-pretrained-models-install.md)。 |

## <a name="using-a-standalone-server"></a>使用獨立伺服器

R 和 Python 開發人員通常會選擇獨立伺服器，以超越開放原始碼 R 和 Python 的記憶體和處理條件約束。 在獨立伺服器上執行的 R 和 Python 程式庫，可以在多個核心上載入和處理大量資料，並將結果彙總成單一合併輸出。 高效能功能是針對規模和公用程式而設計：在商務伺服器產品中提供預測性分析、統計模型、資料視覺效果和領先業界的機器學習演算法，並且受到 Microsoft 支援。

隨著獨立伺服器與 SQL Server 分離，R 和 Python 環境會使用基礎作業系統和獨立伺服器 (而不是 SQL Server) 中提供的標準工具進行設定、保護和存取。 SQL Server 關聯式資料並沒有內建支援。 如果想要使用 SQL Server 資料，您可以建立資料來源物件和連接，就像從任何用戶端所做的一樣。

如果您同時需要本機和遠端計算，獨立伺服器也可以當成 SQL Server 的附屬電腦，作為強大的開發環境。 獨立伺服器上的 R 和 Python 套件與資料庫引擎安裝所提供的套件相同，允許程式碼可攜性和[計算內容切換](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)。

## <a name="how-to-get-started"></a>如何開始使用

從安裝開始，將二進位檔附加至您最愛的開發工具，並撰寫您的第一個指令碼。

### <a name="step-1-install-the-software"></a>步驟 1:安裝軟體

安裝下列其中一個版本：

+ [SQL Server 2017 Machine Learning Server (獨立式)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R 伺服器 (獨立式) - 僅限 R](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>步驟 2:設定開發工具

在獨立伺服器上，通常會使用安裝在同一部電腦上的開發，在本機上工作。

+ [設定 R 工具](set-up-a-data-science-client.md)
+ [設定 Python 工具](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>步驟 3：撰寫您的第一個指令碼

使用來自 RevoScaleR、revoscalepy 和機器學習演算法的函式來撰寫 R 或 Python 指令碼。
  
  + [在 25 個函式中探索 R 和 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler) (英文)：開始使用基本 R 命令，然後進行 RevoScaleR 可散發分析函式，以提供高效能 R 解決方案以及進行調整。 包含許多最熱門 R 模型建立套件 (例如 	K-Means 叢集、決策樹及決策樹系) 的可平行處理版本，以及資料操作工具。

  + [快速入門：使用 microsoftml Python 套件的二元分類範例](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml) (英文)：使用來自 microsoftml 的函式和已知的乳癌資料集，建立二元分類模型。

選擇工作的最佳語言。 R 最適合難以使用 SQL 來實作的統計計算。 對於資料的集合型作業，請利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的能力來達到最大效能。 使用記憶體內部資料庫引擎，以快速計算資料行。

### <a name="step-4-operationalize-your-solution"></a>步驟 4：讓您的解決方案運作

獨立伺服器可以使用非 SQL 品牌 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server) (英文) 的 [運作化](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) (英文) 功能。 您可以設定獨立伺服器以運作，其具備以 Web 服務形式部署和裝載程式碼、執行診斷、測試 Web 服務容量等優點。

### <a name="step-5-maintain-your-server"></a>步驟 5：維護您的伺服器

SQL Server 會定期發佈累積更新。 套用累積更新可增加現有安裝的安全性和功能增強功能。 

如需新增或變更功能的說明，請參閱 [CAB 下載](../install/sql-ml-cab-downloads.md)一文和 [SQL Server 2016 累積更新](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions)和 [SQL Server 2017 累積更新](https://support.microsoft.com/help/4047329)的網頁。 

如需如何將更新套用至現有執行個體的詳細資訊，請參閱安裝指示中的[套用更新](../install/sql-machine-learning-standalone-windows-install.md#apply-cu)。

## <a name="see-also"></a>另請參閱

 [安裝 R 伺服器 (獨立式) 或 Machine Learning Server (獨立式)](../install/sql-machine-learning-standalone-windows-install.md)

