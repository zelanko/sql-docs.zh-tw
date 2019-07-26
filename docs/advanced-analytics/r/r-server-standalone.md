---
title: 獨立 R Server 或 Machine Learning Server 安裝
description: SQL Server 設定中的獨立 R 伺服器和 Machine Learning Server 簡介
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: overview
author: dphansen
ms.author: davidph
ms.openlocfilehash: 84ef5d684e767016491baa6e47e37d1402fc6879
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470051"
---
# <a name="r-server-standalone-and-machine-learning-server-standalone-in-sql-server"></a>SQL Server 中的 R Server (獨立式) 和 Machine Learning Server (獨立式)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 提供獨立 R 伺服器的安裝支援, 或獨立于 SQL Server 執行的 Machine Learning Server。 根據您的 SQL Server 版本而定, 獨立伺服器具有開放原始碼 R 和可能 Python 的基礎, 並與 Microsoft 中的高效能程式庫重迭, 以新增大規模的統計和預測性分析。 程式庫也會啟用在 R 或 Python 中編寫腳本的機器學習工作。 

在 SQL Server 2016 中, 這項功能稱為**r Server (獨立式)** , 而且是僅限 r。 在 SQL Server 2017 中, 它稱為**Machine Learning Server (獨立式)** , 並同時包含 R 和 Python。  

> [!Note]
> 如 SQL Server 安裝程式所安裝, 獨立伺服器在功能上相當於非 SQL 品牌版本的[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), 支援相同的使用者案例, 包括遠端執行、運算化和 web服務, 以及 R 和 Python 程式庫的完整集合。

## <a name="components"></a>元件

SQL Server 2016 僅限 R。 SQL Server 2017 支援 R 和 Python。 下表描述每個版本的功能。

| 元件 | 描述 |
|-----------|-------------|
| R 套件 | [**RevoScaleR**](ref-r-revoscaler.md)是可調整 R 的主要程式庫, 具有用於資料操作、轉換、視覺化和分析的功能。  <br/>[**MicrosoftML**](ref-r-microsoftml.md)會新增機器學習演算法, 以建立文字分析、影像分析和情感分析的自訂模型。 <br/>[**sqlRUtils**](ref-r-sqlrutils.md)提供 helper 函式, 可將 R 腳本放入 t-sql 預存程式、向資料庫註冊預存程式, 以及從 R 開發環境執行預存程式。<br/>[**mrsdeploy**](operationalization-with-mrsdeploy.md)提供 web 服務部署 (僅限 SQL Server 2017)。 <br/>[**olapR**](ref-r-olapr.md)是用來在 R 中指定 MDX 查詢。|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open)是 Microsoft 的 R 開放原始碼散發。包含封裝和解譯器。 請一律使用安裝程式中配套的 MRO 版本。 |
| R 工具 | R 主控台視窗和命令提示字元是 R 散發套件中的標準工具。 在 \Program files\Microsoft SQL Server\140\R_SERVER\bin\x64. 尋找這些專案 |
| R 範例和腳本 |  開放原始碼 R 和 RevoScaleR 套件包含內建的資料集, 讓您可以使用預先安裝的資料來建立和執行腳本。 在 \Program files\Microsoft SQL Server\140\R_SERVER\library\datasets 和 \library\RevoScaleR. 尋找這些專案 |
| Python 套件 | [**revoscalepy**](../python/ref-py-revoscalepy.md)是可調整 Python 的主要程式庫, 其中包含用於資料操作、轉換、視覺化和分析的功能。 <br/>[**microsoftml**](../python/ref-py-microsoftml.md)會新增機器學習演算法, 以建立文字分析、影像分析和情感分析的自訂模型。  |
| Python 工具 | 內建的 Python 命令列工具適用于臨機操作測試和工作。 在 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\python.exe. 尋找此工具 |
| Anaconda | Anaconda 是 Python 和基本套件的開放原始碼散發。 |
| Python 範例和腳本 | 如同 R, Python 包含內建的資料集和腳本。 在 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data. 尋找 revoscalepy 資料 |
| R 和 Python 中預先定型的模型 | 預先定型的模型是針對特定使用案例所建立, 並由 Microsoft 的資料科學工程團隊進行維護。 您可以使用您所提供的新資料輸入, 依實際情況使用預先定型的模型來對文字中的正負情感進行評分, 或偵測影像中的特徵。 預先定型的模型在獨立伺服器上支援和使用, 但是您無法透過 SQL Server 安裝程式來安裝。 如需詳細資訊, 請參閱[在 SQL Server 上安裝預先定型機器學習模型](../install/sql-pretrained-models-install.md)。 |

## <a name="using-a-standalone-server"></a>使用獨立伺服器

R 和 Python 開發人員通常會選擇獨立伺服器, 以超越開放原始碼 R 和 Python 的記憶體和處理條件約束。 在獨立伺服器上執行的 R 和 Python 程式庫, 可以在多個核心上載入和處理大量資料, 並將結果匯總成單一合併輸出。 高效能功能是針對規模和公用程式而設計: 在商務服務器產品中提供預測性分析、統計模型、資料視覺效果和領先業界的機器學習服務演算法, 並支援Microsoft.

隨著獨立伺服器與 SQL Server 分離, R 和 Python 環境已設定、受到保護, 並使用獨立伺服器提供的基礎作業系統和標準工具進行存取, 而不是 SQL Server。 SQL Server 關聯式資料並沒有內建支援。 如果您想要使用 SQL Server 的資料, 您可以建立資料來源物件和連接, 就像從任何用戶端一樣。

如果您同時需要本機和遠端運算, 獨立伺服器也可以做為 SQL Server 的附屬電腦, 做為強大的開發環境。 獨立伺服器上的 R 和 Python 封裝與 database engine 安裝所提供的套件相同, 允許進行程式碼可攜性和[計算內容切換](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)。

## <a name="how-to-get-started"></a>如何開始使用

從安裝程式開始, 將二進位檔附加至您最愛的開發工具, 並撰寫您的第一個腳本。

### <a name="step-1-install-the-software"></a>步驟 1：安裝軟體

安裝下列其中一個版本:

+ [SQL Server 2017 Machine Learning Server (獨立)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (獨立式)-僅限 R](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>步驟 2：設定開發工具

在獨立伺服器上, 通常會使用安裝在同一部電腦上的開發, 在本機上工作。

+ [設定 R 工具](set-up-a-data-science-client.md)
+ [設定 Python 工具](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>步驟 3：撰寫您的第一個腳本

使用來自 RevoScaleR、revoscalepy 和機器學習演算法的函式來撰寫 R 或 Python 腳本。
  
  + [探索在25個函數中的 R 和 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler):開始使用基本 R 命令, 然後進行 RevoScaleR 可散發分析函式的進度, 以提供高效能和調整 R 解決方案。 包含許多最熱門 R 模型建立套件 (例如 	K-Means 叢集、決策樹及決策樹系) 的可平行處理版本，以及資料操作工具。

  + [入門使用 microsoftml Python 套件](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml)進行二元分類的範例:使用來自 microsoftml 的函式和知名的乳癌癌症資料集, 建立二元分類模型。

選擇工作的最佳語言。 R 適用于難以使用 SQL 來執行的統計計算。 對於資料的集合型作業, 請利用的功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]來達到最大效能。 使用記憶體內部資料庫引擎, 以快速計算資料行。

### <a name="step-4-operationalize-your-solution"></a>步驟 4：讓您的解決方案

獨立伺服器可以使用非 SQL 品牌[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)的[運算化](https://docs.microsoft.com//machine-learning-server/what-is-operationalization)功能。 您可以為運算化設定獨立伺服器, 以提供下列優點: 將程式碼部署和裝載為 web 服務、執行診斷、測試 web 服務容量。

### <a name="step-5-maintain-your-server"></a>步驟 5：維護您的伺服器

SQL Server 定期釋放累計更新。 套用累計更新可增加現有安裝的安全性和功能增強功能。 

如需新增或變更功能的說明, 請參閱[CAB 下載](../install/sql-ml-cab-downloads.md)文章和[SQL Server 2016 累積更新](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions)的網頁和[SQL Server 2017 累計更新](https://support.microsoft.com/help/4047329)。 

如需如何將更新套用至現有實例的詳細資訊, 請參閱安裝指示中的套用[更新](../install/sql-machine-learning-standalone-windows-install.md#apply-cu)。

## <a name="see-also"></a>另請參閱

 [安裝 R Server (獨立式) 或 Machine Learning Server (獨立式)](../install/sql-machine-learning-standalone-windows-install.md)

