---
title: 資料科學解決方案範本
description: 此文章描述示範最佳做法的產業特定範本，並提供可協助您實作機器學習解決方案的建置組塊。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: e7d7b36c2c19d48fec393e38c741244f6713dcd3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470629"
---
# <a name="data-science-scenarios-and-solution-templates"></a>資料科學案例和解決方案範本
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

此文章描述數個 SQL Server 機器學習服務解決方案範本。 這些範本示範最佳做法，並提供可協助您快速實作機器學習解決方案的建置組塊。 每個範本都是針對特定類別或產業來解決特定資料科學問題而設計的。
每個範本所包含的工作，從資料準備和特徵工程，到模型定型和計分，應有盡有。 

::: moniker range="=sql-server-2016"
使用這些範本來了解 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的運作方式。 然後，您可以隨意自訂範本以符合自己的案例，並建置自訂解決方案。
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15"
使用這些範本來了解 SQL Server 機器學習服務的運作方式。 然後，您可以隨意自訂範本以符合自己的案例，並建置自訂解決方案。
::: moniker-end

每個解決方案都包含範例資料、R 程式碼或 Python 程式碼，以及 SQL 預存程序 (如果適用的話)。 您可以在慣用的 R 或 Python 開發環境中執行程式碼，並在 SQL Server 中進行計算。 在某些情況下，您可以使用 T-SQL 和任何 SQL 用戶端工具 (例如 SQL Server Management Studio) 直接執行程式碼。

> [!TIP]
> 
> 大部分的範本都隨附多個版本，同時支援機器學習的內部部署和雲端平台。 例如，您可以只使用 SQL Server 建置解決方案，也可以在 Microsoft R Server 或 Azure Machine Learning 中建置解決方案。

+ 如需下載和安裝指示，請參閱[如何使用範本](#bkmk_HowTo)。

## <a name="fraud-detection"></a>詐騙偵測

[線上詐騙偵測範本 (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**對象：** 偵測詐騙交易的功能對線上商務而言很重要。 為了減少退款損失，企業必須快速找出使用遭竊付款方式或認證進行的交易。 發現詐騙交易時，企業通常會盡快採取措施來封鎖特定帳戶，以避免進一歩損失。 在此案例中，您會了解如何使用線上購物交易資料來識別可能的詐騙。

**方式：** 詐騙偵測會當作二元分類問題來解決。 此範本中所使用的方法可輕易地應用在其他網域中的詐騙偵測。


## <a name="campaign-optimization"></a>行銷活動最佳化

[預測聯絡潛在客戶的方式和時機](https://microsoft.github.io/r-server-campaign-optimization/)

**對象：** 此解決方案使用保險產業資料，根據人口統計、歷程記錄回應資料和產品特定詳細資料來預測潛在客戶。  也會產生建議，以指出接觸使用者以影響購買行為的最佳頻道和時間。

**方式：** 解決方案會建立並比較多個模型。 此解決方案也會示範使用預存程序的自動化資料整合和資料準備。 平行範例是針對資料庫內、Azure 和 HDInsight Spark 中的 SQL Server 所提供。 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>醫療保健：預測停留在醫院的時間長度 

[預測停留在醫院的時間長度](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**對象：** 準確預測哪些患者可能需要長期住院治療，是護理和規劃的重要部分。 系統管理員必須能夠判斷哪些設施需要更多資源，而護理人員希望確保他們可以符合患者的需求。

**方式：** 此解決方案會使用資料科學虛擬機器，並包含已啟用機器學習的 SQL Server 執行個體。 它也包含一組 Power BI 報告，可讓您用來與已部署的模型互動。

## <a name="customer-churn"></a>客戶流失

[客戶流失偵測範本 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**對象：** 分析及預測客戶流失對任何產業都很重要，無論是銀行業、電信業和零售業等等，都必須管理及防止客戶流失到競爭對手處。 客戶流失分析的目標是為了識別哪些客戶可能流失，然後採取適當動作，以留下這類客戶並保持業務往來。

**方式：** 此範本會將流失問題制訂為 **二元分類** 問題。 它使用兩個來源 (客戶人口統計和客戶交易) 中的範例資料，將客戶分類為可能流失或不可能流失。
  
## <a name="predictive-maintenance"></a>預測性維護

[預測性維護範本 (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**對象：** 預測性維護的目標是藉由擷取過去的故障資訊，並使用該資訊來預測裝置何時或何處可能會故障，來提升維護工作的效率。 針對依賴分散式資料或感應器的應用程式，預測裝置過時的功能特別有用。 這個方法也可以套用來監視或預測 IoT (物聯網) 裝置中的錯誤。

**方式：** 此解決方案主要在回答「運行中的電腦何時故障」的問題。 輸入資料代表飛機引擎的模擬感應器度量。 此資料是透過監視引擎的目前作業狀況來取得 (例如目前的工作週期、設定和感應器度量)，可用來建立三種預測模型類型：

-   **迴歸模型**：預測引擎故障前的持續時間。 此範例模型預測「剩餘使用年限」(Remaining Useful Life，RUL) 計量，也稱為「故障時間」(Time to Failure，TTF)。
  
-   **分類模型**：預測引擎是否可能會故障。
  
    **二元分類模型**：預測引擎是否會在特定時間範圍內故障。

    **多類別分類模型**：預測特定引擎是否會故障，並且提供可能的故障時間範圍。 例如，在指定日期下，您可以預測任何裝置可能在該指定日期故障，還是在該指定日期過一段時間後故障。

## <a name="energy-demand-forecasting"></a>能源需求預測

[能源需求預測範本 (SQL Server R Services)](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**何事：** 需求預測是各種領域 (包括能源、零售和服務) 中的重要問題。 精確的需求預測可協助公司進行更佳的生產規劃、資源配置，並做出其他重要的商務決策。 在能源部門中，需求預測對於降低能源儲存成本和平衡供應和需求非常重要。

**方式：** 此範本使用 SQL Server R Services 來預測電力需求。 用於預測的模型是以 **rxDForest** 為基礎的隨機樹系迴歸模型，這是 Microsoft R Server 隨附的高效能機器學習演算法。 此解決方案包含需求模擬器、定型模型需要的所有 R 和 T-SQL 程式碼，以及您可以用來產生及報告預測的預存程序。 


## <a name="how-to-use-the-templates"></a><a name="bkmk_HowTo"></a>如何使用範本

若要下載每個範本中所包含的檔案，您可以使用 GitHub 命令，或開啟連結，然後按一下 [Download Zip (下載 Zip)]  將所有檔案儲存至您的電腦。  下載後的解決方案通常會包含下列資料夾：
  
-   **Data**︰包含每個應用程式的範例資料。
  
-   **R**：包含解決方案需要的所有 R 開發程式碼。 解決方案需要由 Microsoft R Server 提供，但可在任何 R IDE 中開啟及編輯的程式庫。 R 程式碼已經過最佳化，藉由將計算內容設定為 SQL Server 執行個體，以便在「資料庫內」執行計算。
  
-   **SQLR**：包含多個 .sql 檔案，您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 等 SQL 環境中執行這些檔案來建立預存程序，以便執行資料處理、特徵工程和模型部署等相關工作。
  
    此資料夾也包含 PowerShell 指令碼，可加以執行來叫用所有指令碼，並建立端對端環境。 請務必編輯此指令碼，以符合您的環境。

## <a name="next-steps"></a>後續步驟

+ [Python 教學課程](./python-tutorials.md)
+ [R 教學課程](./r-tutorials.md)