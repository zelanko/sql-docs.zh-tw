---
title: SQL Server Machine Learning 服務教學課程 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b692b9660c3caec18c689f56ba382f8df194a9cc
ms.sourcegitcommit: b1990ec4491b5a8097c3675334009cb2876673ef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/17/2018
ms.locfileid: "49384123"
---
# <a name="tutorials-for-sql-server-machine-learning-services"></a>適用於 SQL Server 機器學習服務教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章提供教學課程、 示範和範例應用程式，使用 SQL Server 2016 或 SQL Server 2017 中的機器學習服務功能的完整清單。 從這裡開始，若要了解如何從 T-SQL 執行 R 或 Python、 如何使用遠端和本機計算內容，以及如何最佳化您 SQL 生產環境中的 R 和 Python 程式碼。

+ [Python 教學課程](../tutorials/sql-server-python-tutorials.md)

+ [R 教學課程](../tutorials/sql-server-r-tutorials.md)

如需有關需求以及如何進行設定的詳細資訊，請參閱[必要條件](#bkmk_prerequisites)。

## <a name="samples-and-solutions"></a>範例和解決方案

+ [範例](#bkmk_samples) 

    從 SQL Server 開發團隊這些真實世界案例示範如何內嵌在應用程式中的機器學習服務。 所有的範例包括在生產環境中的程式碼，您可以下載、 修改及使用。

+ [方案](#bkmk_solutions) 

    Microsoft 資料科學小組的範本是可自訂，可讓您快速開始使用機器學習服務。 每個解決方案量身打造的特定工作或業界的問題。 大部分的解決方案被設計來在 SQL Server，或在 Azure 機器學習服務等雲端環境中執行。 其他解決方案可以執行在 Linux 上，或在 Spark 或 Hadoop 叢集中，使用 Microsoft R Server 或 Machine Learning Server。

### <a name ="bkmk_samples"></a>SQL Server 產品範例

這些範例和 SQL Server 和 R Server 的開發小組所提供的示範反白顯示您可以在真實世界應用程式中使用內嵌的分析方式。

| 連結 | 描述 | 適用對象 |
|------|-------------|------------|
| [執行客戶使用 R 和 SQL Server 叢集](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 使用非監督式的學習來區分客戶的銷售資料為基礎。 此範例會使用 Microsoft R 的可調整的 rxKmeans 演算法來建立群集模型。 | SQL Server 2016 或 SQL Server 2017 |
| [執行客戶使用 Python 和 SQL Server 叢集](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | 了解如何使用 Kmeans 演算法來執行非監督式叢集的客戶。 此範例會使用 Python 語言中的資料庫。| SQL Server 2017 |
| [使用 R 和 SQL Server 的預測性模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | 了解如何使用 ski 租賃業務的機器學習服務預測未來，它可以幫助商務計劃和人員滿足未來需求。 此範例會使用的 Microsoft 演算法來建置羅吉斯迴歸 」 和 「 決策樹模型。 | SQL Server 2016 或 SQL Server 2017 |
| [使用 Python 和 SQL Server 的預測性模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | 建置使用 Python，來協助您規劃的未來需求 ski 出租分析應用程式。 這個範例會使用新的 Python 程式庫， **revoscalepy**，以建立線性迴歸模型。 | SQL Server 2017 |
| [如何使用 SQL Server Machine Learning 服務的 Tableau](https://blogs.msdn.microsoft.com/mlserver/2017/12/14/how-to-use-tableau-with-sql-server-machine-learning-services-with-r-and-python/) | 分析社交媒體和建立使用 SQL Server 和 r 的 Tableau 圖形 | SQL Server 2016 或 SQL Server 2017 |

### <a name="bkmk_solutions"></a>解決方案範本

Microsoft 資料科學小組提供的解決方案範本，可用來快速啟動的常見案例的解決方案。 提供所有的程式碼，以及如何定型和部署的模型評分使用 SQL Server 預存程序的指示。

+ [詐騙偵測](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [自訂變換預測](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [預測性維護](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [預測醫院](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

如需詳細資訊，請參閱 [Machine Learning Templates with SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/) (SQL Server 2016 R 服務的機器學習範本)。

## <a name="more-resources-and-reading"></a>更多的資源和讀取

+ [我們為什麼沒有建置它？](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/01/10/sql-server-r-services-why-did-we-build-it/)

    想知道 R Services 背後真正的故事嗎？ 請閱讀此文章說明來源與目標 SQL Server R services 的 PM 小組與開發。

+ [教學課程和 Microsoft R 的範例資料](https://docs.microsoft.com/machine-learning-server/r/tutorial-introduction)

    了解 Microsoft R，以及 RevoScaleR 封裝提供的快速教學課程的這個集合中。 了解如何撰寫 R 程式碼一次，並隨時隨地部署使用 RevoScaleR 的資料來源和遠端計算內容。

+ [開始使用 MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)

  了解如何使用 MicrosoftML 套件中的新演算法的進階模型化和可調整的資料轉換，適用於多個計算內容。
