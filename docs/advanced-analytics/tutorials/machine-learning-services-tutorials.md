---
title: "SQL Server 機器學習教學課程 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- Python
ms.assetid: 5ccc75f6-6703-47d9-b879-9a740569b45e
caps.latest.revision: 32
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0ebeae12d6987154baa7ccb7c9417e9f92b2bbe0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-machine-learning-tutorials"></a>SQL Server 機器學習教學課程

本文提供教學課程、 示範和範例應用程式，以使用 SQL Server 2016 中 SQL Server 2017 機器學習功能的完整的清單。 從這裡開始，以了解如何從 T-SQL 執行 R 或 Python、 使用的遠端和本機計算內容，以及最佳化程式碼 R 和 Python SQL 的生產環境。

## <a name="start-here"></a>入門

+ [Python 教學課程](../tutorials/sql-server-python-tutorials.md)

+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)

如需需求和如何取得設定的詳細資訊，請參閱[必要條件](#bkmk_prerequisites)。

## <a name="samples-and-solutions"></a>範例和解決方案

+ [範例](#bkmk_samples) 

    從 SQL Server 開發團隊這些真實世界案例示範如何內嵌在應用程式中的機器學習。 所有範例都包含在生產環境中的程式碼，您可以下載、 修改及使用。

+ [方案](#bkmk_solutions) 

    從 Microsoft 資料科學小組的範本是可自訂，可協助您快速入門機器學習。 每個解決方案適合特定工作或產業問題;此外，大部分的解決方案被設計來在 SQL Server 或在雲端環境，例如 Azure Machine Learning 中執行。 Microsoft R Server 或 HDI Spark 叢集上執行其他方案。

### <a name ="bkmk_samples"></a>SQL Server 產品範例

這些範例和 SQL Server 和 R Server 開發團隊所提供的示範反白顯示您可以在真實世界應用程式中使用內嵌的分析方式。

+ [執行客戶群集使用 R 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/)

  使用不受監督的學習，根據銷售資料的區段客戶。 此範例會使用 Microsoft 的可擴充 rxKmeans 演算法來建立群集模型。 
  
  適用於： SQL Server 2016 或 SQL Server 2017

+ [新功能 ！執行客戶群集使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    了解如何使用 Kmeans 演算法來執行不受監督的群集的客戶。 這個範例會使用 Python 語言中的資料庫。 
    
    適用於： SQL Server 2017

+ [建置使用 R 和 SQL Server 的預測模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

  了解 ski 以租用方式佔用企業可能會使用機器學習來預測未來出租，它可以幫助商務計劃和人員，以符合未來的要求。 此範例會使用 Microsoft R 演算法來建立羅吉斯迴歸和決策樹模型。 
  
  適用於： SQL Server 2016 或 SQL Server 2017

+ [建置預測模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

   建置 ski 以租用方式佔用分析應用程式使用 Python，協助規劃未來的要求。 這個範例會使用新的 Python 程式庫， **revoscalepy**，以建立線性迴歸模型。 
   
   適用於： SQL Server 2017

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

+ [教學課程和範例 Microsoft R 的資料](https://docs.microsoft.com/r-server/r/tutorial-introduction)

    了解 Microsoft R 以及 RevoScaleR 封裝提供的快速教學課程的這個集合中。 了解如何撰寫一次的 R 程式碼以及部署任何地方，使用 RevoScaleR 資料來源和遠端計算內容。

+ [開始使用 MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

  了解如何使用 MicrosoftML 封裝中的新演算法的進階的模型和可擴充的資料轉換，適合多個計算內容。

## <a name="bkmk_Prerequisites"></a>必要條件

若要執行這些教學課程，您必須下載並安裝 SQL Server 機器學習的元件，如下所示：

+ [設定 SQL Server R 服務](../r/set-up-sql-server-r-services-in-database.md)
+ [設定 SQL Server Python 的服務](../python/setup-python-machine-learning-services.md)

使用 SQL Server 2017，您可以安裝 R 或 Python，或兩者。 否則整體的安裝程序、 架構和需求都相同。

執行 SQL Server 安裝程式，別忘了下列重要步驟：

1. 執行啟用外部指令碼執行功能`sp_configure 'external scripts enabled', 1`。 請依照下列指示重新設定並重新啟動 SQL Server。
2. 請確認啟動控制板服務正在執行，然後，背景工作使用的帳戶就可以連接到 SQL Server 執行個體。
3. 檢閱 SQL 登入和執行 R 或 Python 指令碼的 Windows 使用者帳戶相關聯的權限。 所有需要權限來執行 R 或 Python 指令碼，並將連接到執行個體。 根據此範例中，它們可能也需要讀取和寫入資料，以及建立資料庫物件的權限。

如需詳細資訊，請參閱本文的一些常見的安裝和組態問題：[疑難排解機器學習服務](../machine-learning-troubleshooting-faq.md)

> [!NOTE]
> 您無法執行這些教學課程中使用另一個開放原始碼 R 或 Python 工具。 您的開發環境和機器學習服務與 SQL Server 電腦都必須有 R 或 Python 提供的程式庫的 Microsoft 支援與 SQL Server 和使用遠端計算內容的整合。

