---
title: SQL Server R 和 Python 教學課程-SQL Server Machine Learning
description: 範例和教學課程對 R 和 Python 中 SQL Server 機器學習服務指令碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2b30daadd23cbea244576c461ec783e67b2189cf
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511045"
---
# <a name="sql-server-machine-learning-tutorials-in-r-and-python"></a>R 和 Python 中的 SQL Server 機器學習服務教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章提供教學課程和程式碼範例示範的機器學習服務功能的完整清單[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)或是[SQL Server 2017 Machine Learning 的服務](../install/sql-machine-learning-services-windows-install.md)。 

+ 快速入門會使用最少心力快速瀏覽使用內建的資料或任何資料。
+ 教學課程會深入多個工作、 與較大型資料集，較長的說明。
+ 範例和解決方案適用於開發人員偏好程式碼，開始進行倒概念和知識補的課程。

您將了解如何使用 R 和 Python 程式庫，與內建的關聯式資料，在相同的運作內容、 如何使用 SQL Server 預存程序來執行和部署自訂的程式碼，以及如何呼叫 Microsoft R 和 Python 程式庫的高效能的資料科學和機器學習工作。

第一個步驟中，檢閱 基本概念，支援 Microsoft R 和 Python 與 SQL Server 的整合。

## <a name="concepts"></a>概念

當您安裝 SQL Server Machine Learning 服務或 SQL Server 2016 R Services (僅 R) 資料庫引擎的附加元件時，資料庫內分析就是指對 R 和 SQL Server 上的 Python 原生支援。 R 和 Python 的整合包括基底的開放原始碼散發套件，再加上高效能分析的 Microsoft 特定程式庫。

從架構小站點，您的程式碼外部處理序上執行的方塊，以保留資料庫引擎的完整性。 不過，所有的資料存取和安全性是透過 SQL Server 資料庫角色和權限，這表示 SQL server 存取的任何應用程式可以存取您的 R 和 Python 指令碼，當您部署預存程序中，或序列化，並將定型的模型儲存至 SQL伺服器資料庫。

SQL Server 上支援與其他 Microsoft 產品中的對等的語言支援的 R 和 Python 的主要差異，而且服務包括：

+ 預存程序或二進位模型的 「 套件 」 程式碼的能力。
+ 撰寫呼叫與 SQL Server 程式檔在本機安裝的 Microsoft R 和 Python 程式庫的程式碼。
+ 套用至 R 和 Python 解決方案的 SQL Server 資料庫安全性架構。
+ 利用 SQL Server 基礎結構和您的自訂解決方案的系統管理支援。

## <a name="quickstarts"></a>快速入門

從這裡開始，若要了解如何從 T-SQL 執行 R 或 Python，以及如何實作您 SQL 生產環境中的 R 和 Python 程式碼。

+ [Python:使用 T-SQL 執行的 Python](run-python-using-t-sql.md)
+ [:在 R 和 SQL 中的 hello World](rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [:處理輸入和輸出](rtsql-working-with-inputs-and-outputs.md)
+ [:處理資料型別和物件](rtsql-r-and-sql-data-types-and-data-objects.md)
+ [:使用 R 函式](rtsql-using-r-functions-with-sql-server-data.md)
+ [:建立預測模型](rtsql-create-a-predictive-model-r.md)
+ [:從模型預測並繪製](rtsql-predict-and-plot-from-model.md)

## <a name="tutorials"></a>教學課程

採取仔細看看 Microsoft 套件和更具特製化的作業，例如從本機轉移到遠端計算內容來建置 R 和 Python 和 T-SQL 您第一次接觸。

+ [Python 教學課程](sql-server-python-tutorials.md)
+ [R 教學課程](sql-server-r-tutorials.md)

<a name ="bkmk_samples"></a>

## <a name="samples"></a>範例

這些範例和 SQL Server 和 R Server 的開發小組所提供的示範反白顯示您可以在真實世界應用程式中使用內嵌的分析方式。

| 連結 | 描述 | 
|------|-------------|
| [執行客戶使用 R 和 SQL Server 叢集](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 使用非監督式的學習來區分客戶的銷售資料為基礎。 此範例會使用 Microsoft R 的可調整的 rxKmeans 演算法來建立群集模型。 |
| [執行客戶使用 Python 和 SQL Server 叢集](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | 了解如何使用 Kmeans 演算法來執行非監督式叢集的客戶。 此範例會使用 Python 語言中的資料庫。| SQL Server 2017 |
| [使用 R 和 SQL Server 的預測性模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | 了解如何使用 ski 租賃業務的機器學習服務預測未來，它可以幫助商務計劃和人員滿足未來需求。 此範例會使用的 Microsoft 演算法來建置羅吉斯迴歸 」 和 「 決策樹模型。 | 
| [使用 Python 和 SQL Server 的預測性模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | 建置使用 Python，來協助您規劃的未來需求 ski 出租分析應用程式。 這個範例會使用新的 Python 程式庫， **revoscalepy**，以建立線性迴歸模型。 | 
| [如何使用 SQL Server Machine Learning 服務的 Tableau](https://blogs.msdn.microsoft.com/mlserver/2017/12/14/how-to-use-tableau-with-sql-server-machine-learning-services-with-r-and-python/) | 分析社交媒體和建立使用 SQL Server 和 r 的 Tableau 圖形 | 

<a name="bkmk_solutions"></a>

## <a name="solution-templates"></a>解決方案範本

Microsoft 資料科學小組提供可自訂的解決方案範本，可用來快速啟動的常見案例的解決方案。 每個解決方案量身打造的特定工作或業界的問題。 大部分的解決方案被設計來在 SQL Server，或在 Azure 機器學習服務等雲端環境中執行。 其他解決方案可以執行在 Linux 上，或在 Spark 或 Hadoop 叢集中，使用 Microsoft R Server 或 Machine Learning Server。

提供所有的程式碼，以及如何定型和部署的模型評分使用 SQL Server 預存程序的指示。

+ [詐騙偵測](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [自訂變換預測](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [預測性維護](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [預測醫院](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

如需詳細資訊，請參閱 [Machine Learning Templates with SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/) (SQL Server 2016 R 服務的機器學習範本)。

