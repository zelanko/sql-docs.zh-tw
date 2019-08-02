---
title: SQL Server R 和 Python 教學課程
description: SQL Server Machine Learning 服務中 R 和 Python 腳本的範例和教學課程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5e05a62be604b9d1a3feeaea1ed4f05dc3538493
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715469"
---
# <a name="sql-server-machine-learning-tutorials-in-r-and-python"></a>R 和 Python 中的 SQL Server Machine Learning 教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文提供教學課程和程式碼範例的完整清單, 示範[SQL Server 2016 R services](../install/sql-r-services-windows-install.md)或[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)的機器學習功能。 

+ 快速入門使用內建資料或無資料, 以最少的方式進行快速探索。
+ 教學課程更深入探討更多工具、較大的資料集和較長的說明。
+ 範例和解決方案適用于偏好以程式碼開始的開發人員, 並回溯至概念和課程, 以填滿知識差距。

您將瞭解如何在相同的操作內容中使用 R 和 Python 程式庫搭配常駐關聯式資料、如何使用 SQL Server 預存程式來執行和部署自訂程式碼, 以及如何呼叫 Microsoft R 和 Python 程式庫來取得高效能資料科學和機器學習工作。

在第一個步驟中, 請參閱支援 Microsoft R 和 Python 與 SQL Server 整合的基本概念。

## <a name="concepts"></a>概念

資料庫內分析指的是當您安裝 SQL Server Machine Learning 服務或 SQL Server 2016 R 服務 (僅限 R) 做為資料庫引擎的附加元件時, SQL Server 上 R 和 Python 的原生支援。 R 和 Python 整合包含基礎開放原始碼散發, 加上 Microsoft 特有的程式庫來進行高效能分析。

從架構的角度來看, 您的程式碼會以外部進程的形式在方塊上執行, 以保留資料庫引擎的完整性。 不過, 所有資料存取和安全性都是透過 SQL Server 資料庫角色和許可權, 這表示任何可存取 SQL Server 的應用程式都可以存取您的 R 和 Python 腳本 (當您將它部署為預存程式時), 或是將定型的模型序列化並儲存至 SQL伺服器資料庫。

R 和 Python 支援 SQL Server 與其他 Microsoft 產品和服務的對等語言支援之間的主要差異包括:

+ 能夠在預存程式或二進位模型中「封裝」程式碼。
+ 撰寫程式碼, 以呼叫本機安裝的 Microsoft R 和 Python 程式庫和 SQL Server 的程式檔案。
+ 將 SQL Server 的資料庫安全性架構套用至您的 R 和 Python 解決方案。
+ 利用您自訂解決方案的 SQL Server 基礎結構和系統管理支援。

## <a name="quickstarts"></a>快速入門

從這裡開始, 以瞭解如何從 T-sql 執行 R 或 Python, 以及如何為 SQL 生產環境讓您的 R 和 Python 程式碼。

+ [Python使用 T-sql 執行 Python](run-python-using-t-sql.md)
+ [RR 和 SQL 中的 Hello World](rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R處理輸入和輸出](rtsql-working-with-inputs-and-outputs.md)
+ [R處理資料類型和物件](rtsql-r-and-sql-data-types-and-data-objects.md)
+ [R使用 R 函數](rtsql-using-r-functions-with-sql-server-data.md)
+ [R建立預測模型](rtsql-create-a-predictive-model-r.md)
+ [R從模型預測及繪製](rtsql-predict-and-plot-from-model.md)

## <a name="tutorials"></a>教學課程

透過使用 R 和 Python 和 T-sql 的第一次體驗, 進一步探討 Microsoft 封裝和更具體的作業, 例如從本機轉移到遠端計算內容。

+ [Python 教學課程](sql-server-python-tutorials.md)
+ [R 教學課程](sql-server-r-tutorials.md)

<a name ="bkmk_samples"></a>

## <a name="samples"></a>範例

SQL Server 和 R 伺服器開發小組所提供的這些範例和示範, 會醒目提示您可以在真實世界應用程式中使用內嵌分析的方式。

| 連結 | 描述 | 
|------|-------------|
| [使用 R 和 SQL Server 執行客戶群集](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 使用不受監督 learning 根據銷售資料來分割客戶。 這個範例會使用 Microsoft R 的可擴充 rxKmeans 演算法來建立叢集模型。 |
| [使用 Python 和 SQL Server 執行客戶叢集](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | 瞭解如何使用 Kmeans 演算法來執行客戶的不受監督叢集。 這個範例會使用資料庫中的 Python 語言。| SQL Server 2017 |
| [使用 R 和 SQL Server 建立預測模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | 瞭解 ski 出租公司如何使用機器學習來預測未來的租用, 以協助商務計畫和員工滿足未來的需求。 這個範例會使用 Microsoft 演算法來建立羅吉斯回歸和決策樹模型。 | 
| [使用 Python 和 SQL Server 建立預測模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | 使用 Python 建立 ski 出租分析應用程式, 以協助規劃未來的需求。 這個範例使用新的 Python 程式庫**revoscalepy**來建立線性回歸模型。 | 

<a name="bkmk_solutions"></a>

## <a name="solution-templates"></a>解決方案範本

Microsoft 資料科學小組已提供可自訂的解決方案範本, 可用來針對常見案例快速啟動解決方案。 每個解決方案都是針對特定工作或產業問題而量身打造。 大部分的解決方案都是設計成在 SQL Server 或雲端環境 (例如 Azure Machine Learning) 中執行。 您可以使用 Microsoft R Server 或 Machine Learning Server, 在 Linux 或 Spark 或 Hadoop 叢集上執行其他解決方案。

會提供所有程式碼, 以及如何使用 SQL Server 的預存程式來定型和部署模型以進行評分的指示。

+ [詐騙偵測](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [自訂變換預測](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [預測性維護](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [預測醫院的持續時間長度](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

