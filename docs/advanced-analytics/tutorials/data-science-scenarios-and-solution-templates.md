---
title: 資料科學案例和解決方案範本
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: e50344bc94f25e6efd8303f93506401448f94fd1
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344728"
---
# <a name="data-science-scenarios-and-solution-templates"></a>資料科學案例和解決方案範本
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

範本是範例解決方案，其示範最佳做法，並提供可協助您快速實作解決方案的建置組塊。 每個範本都是針對特定的垂直或產業來解決特定問題而設計的。 每個範本所包含的工作，從資料準備和特徵工程，到模型定型和計分，應有盡有。 使用這些範本來瞭解如何[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]運作。 然後, 您可以隨意自訂範本以符合您自己的案例, 並建立自訂解決方案。 

每個解決方案都包含範例資料、R 程式碼或 Python 程式碼, 以及 SQL 預存程式 (如果適用的話)。 您可以在慣用的 R 或 Python 開發環境中執行程式碼, 並在 SQL Server 中進行計算。 在某些情況下, 您可以使用 T-sql 和任何 SQL 用戶端工具 (例如 SQL Server Management Studio) 直接執行程式碼。

> [!TIP]
> 
> 大部分的範本都隨附多個版本, 同時支援機器學習服務的內部部署和雲端平臺。 例如, 您可以只使用 SQL Server 建立方案, 或者您可以在 Microsoft R Server 中或在 Azure Machine Learning 中建立解決方案。

+ 如需下載和設定指示, 請參閱[如何使用範本](#bkmk_HowTo)。

## <a name="fraud-detection"></a>詐騙偵測

[線上詐騙偵測範本 (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**我**偵測詐騙交易的功能對線上企業而言很重要。 若要減少回復損失, 企業必須快速找出使用遭竊付款儀器或認證所建立的交易。 發現詐騙交易時，企業通常會盡快採取措施來封鎖特定帳戶，以避免進一歩損失。 在此案例中, 您將瞭解如何使用線上購買交易的資料來識別可能的詐騙。

**程度**詐騙偵測會當作二元分類問題來解決。 此範本中所使用的方法可輕易地應用在其他網域中的詐騙偵測。


## <a name="campaign-optimization"></a>行銷活動優化

[預測聯絡潛在客戶的方式和時機](https://microsoft.github.io/r-server-campaign-optimization/)

**我**此解決方案使用保險產業資料, 根據人口統計、歷程記錄回應資料和產品特定的詳細資料來預測潛在客戶。  也會產生建議, 以指示使用者影響購買行為的最佳頻道和時間。

**程度**解決方案會建立並比較多個模型。 此解決方案也會示範使用預存程式的自動化資料整合和資料準備。 平行範例是針對資料庫內、Azure 和 HDInsight Spark 中的 SQL Server 所提供。 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>醫療保健: 預測持續在醫院中的長度 

[預測持續在醫院中的長度](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**我**準確預測哪些患者可能需要長期 hospitalization, 是護理和規劃的重要部分。 系統管理員必須能夠判斷哪些設施需要更多資源, 而護理人員想要確保他們可以符合病人的需求。

**程度**此解決方案會使用資料科學虛擬機器, 並包含已啟用機器學習服務的 SQL Server 實例。 它也包含一組 Power BI 報表, 可讓您用來與已部署的模型互動。

## <a name="customer-churn"></a>客戶流失

[客戶流失預測範本 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**我**分析和預測客戶流失在任何產業中都很重要, 因為必須管理和避免客戶的遺失: 銀行業、電信和零售等等。 客戶流失分析的目標是為了識別哪些客戶可能流失，然後採取適當動作，以留下這類客戶並保持業務往來。

**程度**此範本會將流失問題會構成為**二元分類**問題。 它使用兩個來源 (客戶人口統計和客戶交易) 中的範例資料，將客戶分類為可能流失或不可能流失。
  
## <a name="predictive-maintenance"></a>預測性維護

[預測性維護範本 (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**我**「預測性維護」的目的是要藉由捕捉過去的失敗並使用該資訊來預測裝置可能失敗的時間或位置, 來提升維護工作的效率。 針對依賴分散式資料或感應器的應用程式, 預測裝置過時的功能特別有用。 這個方法也可以套用來監視或預測 IoT (物聯網) 裝置中的錯誤。

**程度**此解決方案的重點在於回答「何時將服務機器故障？」這個問題。 輸入資料代表飛機引擎的模擬感應器度量。 從監視引擎目前作業條件 (例如目前的工作週期、設定和感應器測量) 取得的資料, 是用來建立三種預測模型類型:

-   **迴歸模型**：預測引擎故障前的持續時間。 範例模型會預測「剩餘有用的生命週期」 (RUL) 度量, 也稱為「失敗時間」 (.TTF)。
  
-   **分類模型**：預測引擎是否可能會故障。
  
    **二元分類模型**會預測引擎是否會在特定時間範圍內失敗。

    **多類別分類模型**會預測特定引擎是否可能失敗, 並提供可能的失敗時間範圍。 例如，在指定日期下，您可以預測任何裝置可能在該指定日期故障，還是在該指定日期過一段時間後故障。

## <a name="energy-demand-forecasting"></a>能源需求預測

[具有 SQL Server R Services 的能源需求預測範本](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**功能:** 需求預測是各種領域 (包括能源、零售和服務) 中的重要問題。 精確的需求預測可協助公司進行更佳的生產規劃、資源配置, 並做出其他重要的商業決策。 在能源部門中, 需求預測對於降低能源儲存成本和平衡供應和需求非常重要。

**程度**此範本會使用 SQL Server R Services 來預測電力需求。 用於預測的模型是以**rxDForest**為基礎的隨機樹系回歸模型, 這是 Microsoft R Server 隨附的高效能機器學習服務演算法。 此解決方案包含需求模擬器、定型模型需要的所有 R 和 T-SQL 程式碼，以及您可以用來產生及報告預測的預存程序。 


## <a name="bkmk_HowTo"></a>如何使用範本

若要下載每個範本中所包含的檔案，您可以使用 GitHub 命令，或開啟連結，然後按一下 [Download Zip (下載 Zip)]  將所有檔案儲存至您的電腦。  下載後的解決方案通常會包含下列資料夾：
  
-   **資料**:包含每個應用程式的範例資料。
  
-   **R**:包含方案所需的所有 R 開發程式碼。 解決方案需要由 Microsoft R Server 提供，但可在任何 R IDE 中開啟及編輯的程式庫。 R 程式碼已經過最佳化，藉由將計算內容設定為 SQL Server 執行個體，以便在「資料庫內」執行計算。
  
-   **SQLR**:包含多個 .sql 檔案, 您可以在等[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sql 環境中執行這些檔案來建立預存程式, 以便執行資料處理、特徵工程和模型部署等相關工作。
  
    此資料夾也包含 PowerShell 指令碼，可加以執行來叫用所有指令碼，並建立端對端環境。 請務必編輯此指令碼，以符合您的環境。

## <a name="next-steps"></a>後續步驟

+ [SQL Server 機器學習服務教學課程](machine-learning-services-tutorials.md)




