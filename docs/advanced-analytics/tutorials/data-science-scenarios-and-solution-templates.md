---
title: "資料科學案例和解決方案範本 |Microsoft 文件"
ms.custom: 
ms.date: 08/22/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
ms.assetid: 49e54fa9-9b28-44ba-b256-06dad4e8dece
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 3c180282735da59d8d3dfa039e70d0eea5ebd7e5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="data-science-scenarios-and-solution-templates"></a>資料科學案例和方案範本

範本是範例解決方案，其示範最佳做法，並提供可協助您快速實作解決方案的建置組塊。 每個範本被設計來解決特定問題，針對特定的垂直或產業。 每個範本所包含的工作，從資料準備和特徵工程，到模型定型和計分，應有盡有。 使用這些範本，若要了解如何[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]的運作方式。 然後，請隨意自訂的範本符合您自己的案例，並建置自訂解決方案。 

每個方案包含範例資料、 R 程式碼或 Python 程式碼，而且如果適用於 SQL 預存程序。 程式碼可以執行慣用 R 或 Python 開發環境中，以完成 SQL Server 中的計算。 在某些情況下，您可以執行的程式碼直接使用 T-SQL 和任何 SQL 用戶端工具，例如 SQL Server Management Studio。

> [!TIP]
> 
> 大部分的範本不支援這兩個內部部署的多個版本中，而且雲端平台機器學習。 比方說，您可以建置使用只有 SQL Server 方案，或您可以建置在 Microsoft R Server，或在 Azure Machine Learning 中的方案。

+ 如需詳細資訊和更新，請參閱這項公告：[率先 Azure ML 中的新範本](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

+ 如需下載和安裝指示，請參閱[如何使用範本](#bkmk_HowTo)。

## <a name="fraud-detection"></a>詐騙偵測

[線上詐騙偵測範本 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)

**項目：**偵測詐騙交易的功能，請務必針對線上企業。 若要降低費用後遺失，企業需要快速識別使用遭竊的支付工具或認證所做的交易。 發現詐騙交易時，企業通常會盡快採取措施來封鎖特定帳戶，以避免進一歩損失。 在此案例中，您會學習如何使用線上購物的交易資料來識別可能的詐騙。

**如何：**為二元分類問題已解決的詐騙偵測。 此範本中所使用的方法可輕易地應用在其他網域中的詐騙偵測。


## <a name="campaign-optimization"></a>行銷活動最佳化

[如何及何時預測潛在客戶的連絡](https://microsoft.github.io/r-server-campaign-optimization/)

**項目：**此解決方案使用保險業資料來預測潛在客戶根據人口統計資料、 歷程記錄的回應資料，以及特定產品的詳細資料。  表示最佳頻道與時間的方法來影響購買行為的使用者，也會產生建議。

**如何：**會建立方案，然後比較多個模型。 解決方案也會示範自動化的資料整合和資料準備使用預存程序。 SQL Server 資料庫內，在 Azure 和 HDInsight Spark 提供平行範例。 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>健康照護： 預測醫院保持狀態的長度 

[醫院保持狀態的預測長度](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**項目：**準確地預測哪些病患可能需要長期住院是小心和計劃很重要的一部分。 系統管理員需要能夠判斷哪些功能需要更多資源，而且 caregivers 想要確保它們可以符合病患的需求。

**如何：**此解決方案使用 Data Science 虛擬機器，而且與啟用的機器學習中包含的 SQL Server 執行個體。 它也包含一組 Power BI 報表，您可以用來與已部署的模型互動。

## <a name="customer-churn"></a>客戶變換

[客戶變換預測範本 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)

**項目：**分析和預測客戶變換量很重要，尤其必須管理及避免競爭對手客戶會遺失任何業界： 銀行、 電信和零售版，等等。 客戶流失分析的目標是為了識別哪些客戶可能流失，然後採取適當動作，以留下這類客戶並保持業務往來。

**如何：**此範本會構成變換問題**二元分類**問題。 它使用兩個來源 (客戶人口統計和客戶交易) 中的範例資料，將客戶分類為可能流失或不可能流失。
  
## <a name="predictive-maintenance"></a>預測性維護

[預測性維護範本 (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/Introduction.md)

**項目：**預測性維護以外的工具來擷取過去的失敗，並使用該資訊來預測時，或其中一個裝置可能會失敗，以增加效率的維護工作。 預測裝置陳舊過時的功能依賴分散式的資料或感應器的應用程式特別有用。 這個方法也無法套用到監視或預測 IoT （物聯網） 裝置中的錯誤。

請參閱此公告，以取得詳細資訊：[新的預測性維護範本](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

**如何：**這個解決方案將著重在回答這個問題，「 時將服務中的電腦失敗？ 」 輸入資料代表飛機引擎的模擬感應器度量。 從監視引擎的目前作業的狀況，目前的工作循環、 設定和感應器的度量，例如取得的資料可用來建立預測模型的三種類型：

-   **迴歸模型**：預測引擎故障前的持續時間。 範例模型來預測"剩餘有用的生命週期 」 (RUL)，也稱為 「 時間來失敗 」 (TTF) 的計量。
  
-   **分類模型**：預測引擎是否可能會故障。
  
    **二元分類模型**預測是否引擎將無法在特定時間範圍內。

    **多級分類模型**預測特定引擎是否可能會失敗，並提供可能的時間窗口失敗。 例如，在指定日期下，您可以預測任何裝置可能在該指定日期故障，還是在該指定日期過一段時間後故障。

## <a name="energy-demand-forecasting"></a>能源需求預測

[能源需求預測範本與 SQL Server R Services](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**項目：**： 需求預測是重要的問題，包括能源、 零售版和服務的各種網域中。 預測正確的要求，可協助公司進行更好的實際執行計劃，資源配置，以及其他重要的商務決策。 在能源磁區需求預測是減少儲存的能源成本並平衡供應和需求的關鍵。

**如何：**此範本來預測需求電力使用 SQL Server R Services。 用於預測的模型為基礎的隨機樹系迴歸模型**rxDForest**、 高效能的機器學習 Microsoft R Server 中所包含的演算法。 此解決方案包含需求模擬器、定型模型需要的所有 R 和 T-SQL 程式碼，以及您可以用來產生及報告預測的預存程序。 


## <a name="bkmk_HowTo"></a>如何使用範本

若要下載每個範本中所包含的檔案，您可以使用 GitHub 命令，或開啟連結，然後按一下 [Download Zip (下載 Zip)] 將所有檔案儲存至您的電腦。  下載後的解決方案通常會包含下列資料夾：
  
-   **Data**︰包含每個應用程式的範例資料。
  
-   **R**︰包含解決方案需要的所有 R 開發程式碼。 解決方案需要由 Microsoft R Server 提供，但可在任何 R IDE 中開啟及編輯的程式庫。 R 程式碼已經過最佳化，藉由將計算內容設定為 SQL Server 執行個體，以便在「資料庫內」執行計算。
  
-   **SQLR**︰包含多個 .sql 檔案，您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 等 SQL 環境中執行這些檔案來建立預存程序，以便執行資料處理、特徵工程和模型部署等相關工作。
  
    此資料夾也包含 PowerShell 指令碼，可加以執行來叫用所有指令碼，並建立端對端環境。 請務必編輯此指令碼，以符合您的環境。

## <a name="next-steps"></a>後續的步驟

+ [SQL Server 機器學習教學課程](machine-learning-services-tutorials.md)




