---
title: SQL Server Python 教學課程 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 541675c22ddbe347f67119d8cba82f75955382e6
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2018
ms.locfileid: "48877982"
---
# <a name="sql-server-python-tutorials"></a>SQL Server Python 教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供一份教學課程和範例，示範如何使用 Python 與 SQL Server 2017。 透過這些範例和示範，您將了解：

+ 如何從 T-SQL 執行 Python
+ 遠端和本機計算內容，和如何執行 Python 程式碼使用 SQL Server 電腦有哪些？
+ 如何將 Python 程式碼包裝在預存程序
+ 最佳化 SQL 生產環境中的 Python 程式碼
+ 內嵌在應用程式中的機器學習服務的真實世界案例

如需需求和安裝資訊，請參閱[必要條件](#bkmk_Prerequisites)。

## <a name="bkmk_pythontutorials"></a>Python 教學課程

+ [在 T-SQL 中執行 Python](run-python-using-t-sql.md)

   了解如何使用 T-SQL 和，於 SQL Server 2016 的擴充性機制中呼叫 Python 的基本概念。

+ [建立機器學習中使用 revoscalepy Python 模型](use-python-revoscalepy-to-create-model.md)

   這一課會示範如何執行程式碼從遠端的 Python 終端機中，使用 SQL Server 計算內容。 您應該略為熟悉 Python 工具和環境。 範例程式碼是提供來建立模型，使用**rxLinMod**，從新**revoscalepy**程式庫。 

+ [適用於 SQL 開發人員的資料庫內 Python 分析](sqldev-in-database-python-for-sql-developers.md)

    此端對端逐步解說示範如何建置完整的 Python 解決方案，使用 T-SQL 預存程序的程序。 包含所有 Python 程式碼都。


## <a name="python-samples"></a>Python 範例

這些範例和 SQL Server 開發團隊所提供的示範反白顯示您可以在真實世界應用程式中使用內嵌的分析方式。

+ [使用 Python 和 SQL Server 的預測性模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  了解如何使用 ski 租賃業務的機器學習服務預測未來，它可以幫助商務計劃和人員滿足未來需求。

  > [!TIP]
  > 現在包含原生評分，從 Python 模型 ！

+ [執行客戶使用 Python 和 SQL Server 叢集](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    了解如何使用 Kmeans 演算法來執行非監督式叢集的客戶。

## <a name="bkmk_Prerequisites"></a>必要條件

若要使用這些教學課程中，您必須擁有 SQL Server 2017，您必須明確地安裝，然後啟用 此功能，Machine Learning 服務 （資料庫）。 

SQL Server 2017 支援 R 和 Python 語言，但未安裝或預設為啟用。 執行 Python 時，需要啟用的擴充性架構，和您要安裝的語言為選取 Python。 

### <a name="post-installation-configuration-tips"></a>安裝後設定秘訣

執行 SQL Server 安裝程式之後, 您可能需要執行一些額外的步驟，以確保 Python 和 SQL Server 進行通訊：

+ 執行啟用外部指令碼執行功能`sp_configure 'external scripts enabled', 1`。
+ 重新啟動伺服器。 
+ 開啟**Services**來檢查是否已啟動 Launchpad 的面板。 
+ 請確定會呼叫外部執行階段的服務具有必要權限。 如需詳細資訊，請參閱 <<c0> [ 啟用隱含的驗證](../security/add-sqlrusergroup-to-database.md)。
+ SQL Server 開啟防火牆上的連接埠，並啟用必要的網路通訊協定。
+ 請確定您的 SQL 登入或 Windows 使用者帳戶具有必要的權限來連接到伺服器，以讀取資料，並建立此範例所需的任何資料庫物件。

請參閱這篇文章的一些常見問題：[疑難排解 Machine Learning 服務](../machine-learning-troubleshooting-faq.md)

### <a name="resource-management"></a>資源管理

您可以在相同的電腦上安裝 R 和 Python 兩者，但同時執行，則可能需要大量資源。 如果您收到 「 記憶體不足 」 錯誤，或如果執行機器學習服務工作主體想要使用的伺服器，您可以減少配置給 database engine 的記憶體數量。 如需詳細資訊，請參閱 <<c0> [ 管理及監視 SQL Server 中的 Python](../python/managing-and-monitoring-python-solutions.md)。

## <a name="see-also"></a>另請參閱

[適用於 SQL Server 的 R 教學課程](sql-server-r-tutorials.md)
