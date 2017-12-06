---
title: "SQL Server 機器學習服務 |Microsoft 文件"
ms.date: 12/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: "38"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 25f508a20cc3e4ff619cc65de67eaae4d9f80bdc
ms.sourcegitcommit: 16347f3f5ed110b5ce4cc47e6ac52b880eba9f5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-machine-learning-services"></a>SQL Server 機器學習服務

SQL Server 2017 機器學習服務 (先前 SQL Server 2016 R Services) 提供開發和部署展現全新深入見解的智慧型應用程式的平台。 因為與整合在機器學習[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以讓分析資料並不需要成本和移動資料相關聯的安全性風險。
  
+ 在 SQL Server 2016 中，您可以輕鬆地開發及部署受歡迎的 R 語言，用於資料科學解決方案。 

    功能包括[Microsoft R](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)程式庫，可提供新的延展性和效能您 R 解決方案中的圖案狀態演算法[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)。
+ 在 SQL Server 2017，您可以使用 R 和 Python 來開發和實施資料科學方案。 

    [Revoscalepy](../python/what-is-revoscalepy.md) Python 程式庫提供遠端計算內容和比較與 RevoScaleR 的延展性。

SQL Server 支援機器學習工作負載透過一組完整的工具和技術提升的效能、 安全性及管理能力。 您可以部署 R 或 Python 方便使用的解決方案、 熟悉 SQL 方法和工具。 只使用[!INCLUDE[tsql](../../includes/tsql-md.md)]呼叫 R 或 Python 執行階段從生產應用程式，來建立模型，或擷取視覺效果。 如果您已經有定型模型，您可以從使用只有 T-SQL，透過它來產生預測[原生計分](../sql-native-scoring.md)。

## <a name="machine-learning-in-sql-server-2017"></a>機器學習中 SQL Server 2017

+ 安裝**機器學習服務 （資料庫）**期間[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上啟用安全地執行 R 或 Python 指令碼安裝程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦。
  
    當您選取這項功能時，擴充功能會安裝 database engine 來支援 R 或 Python 中撰寫的程式碼的執行中。 建立新的服務時，[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]來管理外部執行階段之間的通訊和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。
  
+ 安裝**Microsoft Machine Learning 伺服器 （獨立）**如果您不需要使用 SQL Server 計算內容作為另一部電腦上。 機器學習伺服器包含相同的機器學習服務元件，加上執行做為 web 服務的可擴充、 分散式的機器學習工作的能力。
  
+ 安裝[Microsoft R 用戶端](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)開發解決方案，其中可以部署到 SQL Server，或在 Windows、 Linux 或是 Hadoop 上電腦學習伺服器的遠端電腦上。

## <a name="machine-learning-in-sql-server-2016"></a>機器學習中 SQL Server 2016

+ 安裝**R 服務 （資料庫）**上啟用安全地執行 R 指令碼的 SQL Server 2016 安裝期間[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦。
  
    當您選取這項功能時，您會取得執行 R 指令碼當成計算內容中，使用 SQL Server，或是在預存程序中執行 R 指令碼。
  
+ 安裝**Microsoft R Server （獨立）**從 SQL Server 2016 安裝程式，讓您開發或部署 R 解決方案，您可以使用一部電腦上安裝的 R 元件。

## <a name="how-to-get-started"></a>如何開始

SQL Server 安裝程式會提供兩個選項：

+ 在資料庫分析功能的安裝與 SQL Server 整合，或
+ 安裝支援的 SQL Server 執行個體不在標尺機器學習的獨立版本的機器學習伺服器 （或 Microsoft R Server）。

如果您要執行 R 程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，使用預存程序或使用 SQL Server 執行個體當成計算內容，您必須安裝[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中所述[安裝手冊 》](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。 此選項提供最大資料安全性和 SQL Server 工具與整合。

Microsoft Machine Learning 伺服器 （獨立） 是專為使用所設計的個別選項[Microsoft R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)和[相關 Python 程式庫](../python/what-is-revoscalepy.md)沒有執行 SQL Server 的 Windows 電腦上。 此選項會需要適用於 SQL Server Enterprise Edition 授權。
    
我們建議您在膝上型電腦或其他程式開發中，所使用的遠端電腦上安裝機器學習伺服器 （獨立），並使用該電腦建立和測試的執行個體可以輕鬆部署的機器學習解決方案[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]也就是執行機器學習服務\(中資料庫\)或其他支援計算內容。
  
您也可以使用**mrsdeploy**與機器學習伺服器發行，並將 R，並將 Python 工作發佈為 web 服務一起安裝的封裝。

## <a name="additional-resources"></a>其他資源

+ [開始使用 SQL Server 機器學習服務](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)
 
    描述使用 R 與 SQL Server 的常見案例

+ [設定 SQL Server 機器學習服務或 R 服務資料庫](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

    SQL Server 安裝程式的一部分安裝 R 和相關聯的資料庫元件
  
+ [SQL Server 和 R 教學課程](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    了解如何使用 R 程式碼建立 SQL Server 資料來源，以及如何使用遠端計算內容。 其他以 SQL 開發人員為對象的教學課程會示範如何在 SQL Server 中定型及部署 R 模型。
