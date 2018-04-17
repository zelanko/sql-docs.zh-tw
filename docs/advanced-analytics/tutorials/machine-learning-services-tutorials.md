---
title: SQL Server 機器學習服務教學課程 |Microsoft 文件
ms.date: 12/14/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- Python
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 44f472024d33b68035e3ef5e5dc79c07cc0cff80
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2018
---
# <a name="tutorials-for-sql-server-machine-learning-services"></a>SQL Server 機器學習服務的教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供教學課程、 示範和範例應用程式，以使用 SQL Server 2016 中 SQL Server 2017 機器學習功能的完整的清單。 從這裡開始，若要了解如何從 T-SQL 執行 R 或 Python、 要使用的遠端和本機計算內容，以及如何最佳化程式碼 R 和 Python SQL 的生產環境。

## <a name="start-here"></a>入門

+ [Python 教學課程](../tutorials/sql-server-python-tutorials.md)

+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)

如需需求和如何取得設定的詳細資訊，請參閱[必要條件](#bkmk_prerequisites)。

## <a name="samples-and-solutions"></a>範例和解決方案

+ [範例](#bkmk_samples) 

    從 SQL Server 開發團隊這些真實世界案例示範如何內嵌在應用程式中的機器學習。 所有範例都包含在生產環境中的程式碼，您可以下載、 修改及使用。

+ [方案](#bkmk_solutions) 

    從 Microsoft 資料科學小組的範本是可自訂，可協助您快速入門機器學習。 每個解決方案適合特定工作或產業的問題。 大多數解決方案專為在 SQL Server，或在雲端環境，例如 Azure Machine Learning 中執行。 其他方案可以在 Linux 上或 Spark 或 Hadoop 叢集中，使用執行 Microsoft R Server 機器學習。

### <a name ="bkmk_samples"></a>SQL Server 產品範例

這些範例和 SQL Server 和 R Server 開發團隊所提供的示範反白顯示您可以在真實世界應用程式中使用內嵌的分析方式。

+ [執行客戶群集使用 R 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/)

  使用不受監督的學習，根據銷售資料的區段客戶。 此範例會使用 Microsoft 的可擴充 rxKmeans 演算法來建立群集模型。 
  
  適用於： SQL Server 2016 或 SQL Server 2017

+ [新功能 ！執行客戶群集使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    了解如何使用 Kmeans 演算法來執行不受監督的群集的客戶。 這個範例會使用 Python 語言中的資料庫。
    
    適用於： SQL Server 2017

+ [建置使用 R 和 SQL Server 的預測模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

  了解 ski 以租用方式佔用企業可能會使用機器學習來預測未來出租，它可以幫助商務計劃和人員，以符合未來的要求。 此範例會使用 Microsoft 演算法來建立羅吉斯迴歸和決策樹模型。 
  
  適用於： SQL Server 2016 或 SQL Server 2017

+ [建置預測模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

   建置 ski 以租用方式佔用分析應用程式使用 Python，協助規劃未來的要求。 這個範例會使用新的 Python 程式庫， **revoscalepy**，以建立線性迴歸模型。
   
   適用於： SQL Server 2017

+ [如何使用 SQL Server 機器學習服務 Tableau](https://blogs.msdn.microsoft.com/mlserver/2017/12/14/how-to-use-tableau-with-sql-server-machine-learning-services-with-r-and-python/)

    分析社交媒體及建立 Tableau 圖形，使用 SQL Server 和。

### <a name="bkmk_solutions"></a>方案範本

Microsoft 資料科學團隊提供的解決方案範本，可用來快速啟動常見案例的解決方案。 提供所有的程式碼，以及如何訓練和部署的模型計分使用 SQL Server 預存程序的指示。

+ [詐騙偵測](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [自訂變換預測](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [預測性維護](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [預測保持醫院長度](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

如需詳細資訊，請參閱 [Machine Learning Templates with SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/) (SQL Server 2016 R 服務的機器學習範本)。

## <a name="more-resources-and-reading"></a>更多的資源和讀取

+ [我們為什麼沒有建立它？](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/01/10/sql-server-r-services-why-did-we-build-it/)

    想知道 R Services 背後真正的故事嗎？ 從開發和說明來源和目標 SQL Server R services 的 PM 小組閱讀本文。

+ [教學課程和範例 Microsoft R 的資料](https://docs.microsoft.com/machine-learning-server/r/tutorial-introduction)

    了解 Microsoft R 以及 RevoScaleR 封裝提供的快速教學課程的這個集合中。 了解如何撰寫一次的 R 程式碼以及部署任何地方，使用 RevoScaleR 資料來源和遠端計算內容。

+ [開始使用 MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)

  了解如何使用 MicrosoftML 封裝中的新演算法的進階的模型和可擴充的資料轉換，適合多個計算內容。

## <a name="bkmk_Prerequisites"></a>必要條件

若要執行這些教學課程，您必須下載並安裝 SQL Server 機器學習的元件，如下所示：

+ [安裝 SQL Server 2017 機器學習服務 （資料庫）](../install/sql-machine-learning-services-windows-install.md)
+ [安裝 SQL Server 2016 R Services （資料庫）](../install/sql-r-services-windows-install.md)

使用 SQL Server 2017，您可以安裝 R 或 Python，或兩者。 否則整體的安裝程序、 架構和需求都相同。

執行 SQL Server 安裝程式，別忘了下列重要步驟：

1. 執行啟用外部指令碼執行功能`sp_configure 'external scripts enabled', 1`。 請依照下列指示重新設定並重新啟動 SQL Server。
2. 請確定啟動控制板服務正在執行，然後啟動控制板背景工作帳戶可以連接到 SQL Server 執行個體。
3. 檢閱必須執行 R 或 Python 指令碼的使用者相關聯的權限。 不論您是使用 SQL 登入或 Windows 使用者帳戶，使用者必須擁有執行 R 或 Python 指令碼的權限，且必須能夠連接到執行個體。 取決於教學課程中，使用者可能也需要寫入權限的資料、 建立資料庫物件，或執行大量匯入資料。

如需詳細資訊，請參閱本文的一些常見的安裝和組態問題：[疑難排解機器學習服務](../machine-learning-troubleshooting-faq.md)

> [!NOTE]
> 您無法執行這些教學課程中使用另一個開放原始碼 R 或 Python 工具。 您的開發環境和機器學習服務與 SQL Server 電腦都必須有 R 或 Python 提供的程式庫的 Microsoft 支援與 SQL Server 和使用遠端計算內容的整合。
