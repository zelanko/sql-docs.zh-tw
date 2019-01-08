---
title: 資料科學案例和解決方案範本]-[SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 936bc010838b3869c567117a9e87cdc2c4ce6d52
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596121"
---
# <a name="data-science-scenarios-and-solution-templates"></a>資料科學案例和解決方案範本
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

範本是範例解決方案，其示範最佳做法，並提供可協助您快速實作解決方案的建置組塊。 每個範本被設計來解決特定問題，針對特定的垂直或產業。 每個範本所包含的工作，從資料準備和特徵工程，到模型定型和計分，應有盡有。 若要了解使用這些範本如何[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]的運作方式。 然後，請隨意自訂此範本以符合您自己的案例，並建置自訂解決方案。 

每個方案包含範例資料、 R 程式碼或 Python 程式碼和 SQL 預存程序，如果適用的話。 程式碼可以在完成 SQL Server 中計算的慣用 R 或 Python 開發環境中，執行。 在某些情況下，您可以執行程式碼直接使用 T-SQL 和任何 SQL 用戶端工具，例如 SQL Server Management Studio。

> [!TIP]
> 
> 大部分的範本有多個版本支援這兩個內部部署和雲端平台，適用於 machine learning。 比方說，您可以使用建置解決方案只有 SQL Server，或您可以建置在 Microsoft R Server 中，或在 Azure Machine Learning 中的解決方案。

+ 如需詳細資訊和更新，請參閱本公告：[在 Azure ML 中令人興奮的新範本](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

+ 如需下載和安裝指示，請參閱[如何使用範本](#bkmk_HowTo)。

## <a name="fraud-detection"></a>詐騙偵測

[線上詐騙偵測範本 (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**項目：** 偵測詐騙交易的能力對於線上商務至關重要。 若要減少退款損失，企業需要快速識別使用竊取的付款方式或認證所做的交易。 發現詐騙交易時，企業通常會盡快採取措施來封鎖特定帳戶，以避免進一歩損失。 在此案例中，您將了解如何使用線上購物交易資料來識別可能的詐騙。

**如何：** 詐騙偵測會當作二元分類問題來解決。 此範本中所使用的方法可輕易地應用在其他網域中的詐騙偵測。


## <a name="campaign-optimization"></a>最佳化行銷活動

[預測如何及何時連絡潛在客戶](https://microsoft.github.io/r-server-campaign-optimization/)

**項目：** 此解決方案會使用保險業資料來預測潛在客戶根據人口統計、 歷程記錄的回應資料，以及特定產品的詳細資料。  指出最佳的通道並影響購買行為的使用者方法的時間，也會產生建議。

**如何：** 解決方案會建立，並比較多個模型。 解決方案也會示範自動的資料整合和資料準備使用預存程序。 SQL Server 資料庫，在 Azure 中和 HDInsight Spark 中提供平行的範例。 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>美國衛生保健： 預測長度留在醫院 

[預測住院時間長度](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**項目：** 精準預估的病患可能需要長期住院是照護及規劃的重要部分。 系統管理員需要能夠判斷哪些功能需要更多資源，並看護想要確保他們可以符合病患的需求。

**如何：** 此解決方案會使用資料科學虛擬機器，並利用機器學習服務啟用包含的 SQL Server 執行個體。 它也包含一組 Power BI 報表，您可以使用與已部署的模型進行互動。

## <a name="customer-churn"></a>客戶流失

[客戶流失預測範本 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)

**項目：** 分析及預測客戶流失，請務必在任何產業必須管理及防止客戶流失到競爭對手： 銀行、 電信和零售，等等。 客戶流失分析的目標是為了識別哪些客戶可能流失，然後採取適當動作，以留下這類客戶並保持業務往來。

**如何：** 此範本會構成客戶流失問題以**二元分類**問題。 它使用兩個來源 (客戶人口統計和客戶交易) 中的範例資料，將客戶分類為可能流失或不可能流失。
  
## <a name="predictive-maintenance"></a>預測性維護

[預測性維護範本 (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/Introduction.md)

**項目：** 預測性維護的目標是要提高效率的維護工作，藉由擷取過去的故障，並使用該資訊來預測裝置何時或何處可能會失敗。 預測裝置過時的功能對於依賴分散式的資料或感應器的應用程式特別有用。 這個方法也無法套用到監視或預測 IoT (Internet of Things) 裝置中的錯誤。

此公告，以取得詳細資訊，請參閱：[新的預測性維護範本](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

**如何：** 此解決方案的焦點在於回答問題，「 當將運行中的電腦故障嗎？ 」 輸入資料代表飛機引擎的模擬感應器度量。 取自監視引擎的目前作業狀況，例如目前的工作循環、 設定和感應器測量的資料用來建立預測模型的三種類型：

-   **迴歸模型**：預測引擎故障前的持續時間。 此範例模型會預測 「 剩餘使用年限 」 (RUL)，也稱為 「 時間以失敗 」 (TTF) 的計量。
  
-   **分類模型**：預測引擎是否可能會故障。
  
    **二元分類模型**預測是否引擎將會在特定時間範圍內。

    **多類別分類模型**預測特定引擎是否可能會失敗，並提供失敗的可能時間範圍。 例如，在指定日期下，您可以預測任何裝置可能在該指定日期故障，還是在該指定日期過一段時間後故障。

## <a name="energy-demand-forecasting"></a>能源需求預測

[能源需求預測範本與 SQL Server R Services](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**功能：**:需求預測是重要的問題，包括能源、 零售和服務的各種領域。 精確的需求預測可協助公司進行更好的實際執行計劃，資源配置，並讓其他重要的商業決策。 在能源產業需求預測，對於降低能源儲存體成本和平衡供需重要的。

**如何：** 此範本會使用 SQL Server R Services 來預測電力需求。 用於預測的模型為基礎的隨機樹系迴歸模型**rxDForest**、 高效能機器學習演算法，包含在 Microsoft R Server。 此解決方案包含需求模擬器、定型模型需要的所有 R 和 T-SQL 程式碼，以及您可以用來產生及報告預測的預存程序。 


## <a name="bkmk_HowTo"></a>如何使用範本

若要下載每個範本中所包含的檔案，您可以使用 GitHub 命令，或開啟連結，然後按一下 [Download Zip (下載 Zip)] 將所有檔案儲存至您的電腦。  下載後的解決方案通常會包含下列資料夾：
  
-   **資料**:包含每個應用程式的範例資料。
  
-   **R**:包含解決方案所需的所有 R 開發程式碼。 解決方案需要由 Microsoft R Server 提供，但可在任何 R IDE 中開啟及編輯的程式庫。 R 程式碼已經過最佳化，藉由將計算內容設定為 SQL Server 執行個體，以便在「資料庫內」執行計算。
  
-   **SQLR**:包含多個.sql 檔案可以在 SQL 環境中執行這類[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]若要建立執行相關的工作，例如資料處理的預存程序，特徵工程和模型部署。
  
    此資料夾也包含 PowerShell 指令碼，可加以執行來叫用所有指令碼，並建立端對端環境。 請務必編輯此指令碼，以符合您的環境。

## <a name="next-steps"></a>後續步驟

+ [SQL Server 機器學習服務教學課程](machine-learning-services-tutorials.md)




