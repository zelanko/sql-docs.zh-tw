---
title: 識別您的內部部署資料庫 (Data Migration Assistant) 正確的 Azure SQL 資料庫 SKU |Microsoft Docs
description: 了解如何使用 Data Migration Assistant，以識別您的內部部署資料庫權限的 Azure SQL 資料庫 SKU
ms.custom: ''
ms.date: 05/06/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: 7d87df240d4b83e53ef8f670609d2c896df7fe62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054668"
---
# <a name="identify-the-right-azure-sql-databasemanaged-instance-sku-for-your-on-premises-database"></a>識別您的內部部署資料庫權限的 Azure SQL Database/受控執行個體 SKU

特別是在嘗試為您的資料庫選取最佳的 Azure 資料庫目標和 SKU 時，可能很複雜，將資料庫移轉至雲端。 協助解決這些問題，並讓資料庫移轉體驗更簡單容易藉由提供使用者易記的輸出中的這些 SKU 建議為我們的目標與 Database Migration Assistant (DMA)。

本文著重於 DMA 的 Azure SQL 資料庫 SKU 建議功能。 Azure SQL Database 會有數個部署選項，包括：

- 單一資料庫
- 彈性集區
- 受控執行個體

功能可讓您找出這兩個建議的 Azure SQL Database 單一資料庫的最小的 SKU 建議或從裝載資料庫的電腦收集效能計數器為基礎的 SKU 的受控執行個體。 此功能提供定價層、 計算層級，和最大的資料大小，以及每月預估的成本的相關建議。 它也提供大量佈建單一資料庫和所有的建議資料庫在 Azure 中的 managed 執行個體的能力。

> [!NOTE]
> 才提供此功能目前只能透過命令列介面 (CLI)。

以下是可協助您判斷 Azure SQL 資料庫 SKU 建議和佈建對應的單一資料庫或在 Azure 中使用 DMA 的 managed 執行個體的指示。

## <a name="prerequisites"></a>必要條件

- 下載並安裝最新版[DMA](https://aka.ms/get-dma)。 如果您已經有舊版的工具，開啟它，並將提示您升級 DMA。
- 請確定您的電腦已[PowerShell 版本 5.1](https://www.microsoft.com/download/details.aspx?id=54616)或更新版本中，所需執行所有指令碼。 Findoug 出您的電腦安裝的 PowerShell 版本的相關資訊，請參閱文章[下載並安裝 Windows PowerShell 5.1](https://docs.microsoft.com/skypeforbusiness/set-up-your-computer-for-windows-powershell/download-and-install-windows-powershell-5-1)。
- 請確定您的電腦已安裝 Azure Powershell 模組。 如需詳細資訊，請參閱文章[安裝 Azure PowerShell 模組](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.8.0)。
- 確認 PowerShell 檔案**SkuRecommendationDataCollectionScript.ps1**，這必要項目收集效能計數器，安裝 DMA 資料夾中。
- 請確定您會在其執行此程序的電腦可以裝載您的資料庫之電腦的系統管理員權限。

## <a name="collect-performance-counters"></a>收集效能計數器

此程序的第一個步驟是收集效能計數器，為您的資料庫。 您可以裝載您資料庫的電腦上執行 PowerShell 命令，以收集效能計數器。 DMA 會將您提供一份此 PowerShell 檔案，但是您也可以使用您自己的方法，以從您的電腦擷取效能計數器。

您不需要個別執行每個資料庫的這項工作。 從電腦收集的效能計數器可用來建議的電腦上主控的所有資料庫的 SKU。

1. 在 [DMA] 資料夾中，找出 PowerShell 檔案 SkuRecommendationDataCollectionScript.ps1。 此檔案，才能收集效能計數器。

    ![DMA 資料夾中所示的 PowerShell 檔案](../dma/media/dma-sku-recommend-data-collection-file.png)

2. 執行 PowerShell 指令碼的下列引數：
    - **ComputerName**:裝載您資料庫的電腦名稱。
    - **OutputFilePath**:要儲存所收集的計數器的輸出檔案路徑。
    - **CollectionTimeInSeconds**:在這期間您想要收集效能計數器資料的時間量。 擷取效能計數器，以取得有意義的建議至少 40 分鐘。 擷取的持續時間越長越精準建議會。 也請確定執行的工作負載的所需的資料庫，以便更精確的建議。
    - **DbConnectionString**:指向要從中收集效能計數器資料的電腦上主控的主要資料庫的連接字串。

    以下是範例引動過程：

    ```
    .\SkuRecommendationDataCollectionScript.ps1
     -ComputerName Foobar1
     -OutputFilePath D:\counters2.csv
     -CollectionTimeInSeconds 2400
     -DbConnectionString "Server=localhost;Initial Catalog=master;Integrated Security=SSPI;"
    ```

    命令執行之後，處理程序會輸出檔案，包括效能計數器，以您指定的位置。 您可以使用這個檔案做為輸入，下列程序會提供 SKU 建議為單一資料庫和受管理的執行個體選項的下一個部分。

## <a name="use-the-dma-cli-to-get-sku-recommendations"></a>使用 DMA CLI 取得 SKU 建議

使用您建立效能計數器的輸出檔做為輸入，此程序。

單一資料庫選項時，DMA 會提供 Azure SQL Database 單一資料庫定價層、 計算層級和資料大小上限為每個資料庫在您的電腦上的建議。 如果您在電腦上有多個資料庫，您也可以指定您要為其建議的資料庫。 DMA 也會提供您估計每月成本為每個資料庫。

對於受管理的執行個體，建議會支援並隨即轉移案例。 如此一來，DMA 會為您提供 Azure SQL Database 受控執行個體在電腦上的定價層、 計算層級和一組資料庫的最大的資料大小的建議。 同樣地，如果您在電腦上有多個資料庫，您也可以指定您要為其建議的資料庫。 DMA 也會提供您每月預估成本與受控執行個體。

若要使用 DMA CLI 取得 SKU 的建議，在命令提示字元，請使用下列引數執行 dmacmd.exe:

- **/ 動作 = SkuRecommendation**:輸入這個引數執行 SKU 評量。
- **/ SkuRecommendationInputDataFilePath**:上一節中所收集計數器檔案的路徑。
- **/ SkuRecommendationTsvOutputResultsFilePath**:要寫入以 TSV 格式的輸出結果的路徑。
- **/ SkuRecommendationJsonOutputResultsFilePath**:若要以 JSON 格式寫入輸出結果路徑。
- **/ SkuRecommendationHtmlResultsFilePath**:若要以 HTML 格式寫入輸出結果的路徑。

此外，請選取其中一個下列的引數：

- 防止價格重新整理
  - **/ SkuRecommendationPreventPriceRefresh**:如果設為 True，防止發生價格重新整理，並假設預設的價格。 如果在離線模式中執行，請使用。 如果您不使用這個參數，您必須指定參數來取得指定的區域為基礎的最新價格。
- 取得最新的價格
  - **/ SkuRecommendationCurrencyCode**:要顯示的價格 （例如貨幣「 USD")。
  - **/ SkuRecommendationOfferName**:供應項目名稱 （例如："MS-AZR-0003 P")。 如需詳細資訊，請參閱 < [Microsoft Azure 優惠詳細資料](https://azure.microsoft.com/support/legal/offer-details/)頁面。
    - **/ SkuRecommendationRegionName**:區域名稱 （例如，「 美國西部 」）。
    - **/ SkuRecommendationSubscriptionId**:訂閱識別碼。
    - **/ AzureAuthenticationTenantId**:驗證租用戶中。
    - **/ AzureAuthenticationClientId**:用於驗證的 AAD 應用程式的用戶端識別碼。
    - 其中一個下列的驗證選項：
      - 互動式
        - **AzureAuthenticationInteractiveAuthentication**:設為 true，驗證快顯視窗。
      - 憑證為基礎
        - **AzureAuthenticationCertificateStoreLocation**:設定為 憑證存放區位置 (例如，"CurrentUser")。
        - **AzureAuthenticationCertificateThumbprint**:設定憑證指紋。
      - 基礎語彙基元
        - **AzureAuthenticationToken**:設定憑證的語彙基元。

> [!NOTE]
> 若要取得的 ClientId 和 TenantId 互動式驗證，您需要設定新的 AAD 應用程式。 如需有關驗證和文件中取得這些認證， [Microsoft Azure 計費 API 程式碼範例：RateCard API](https://azure.microsoft.com/resources/samples/billing-python-ratecard-api/)，請遵循下方指示**步驟 1:設定 AAD 租用戶中的原生用戶端應用程式**。

最後，會顯示您可用來指定您想要建議之的資料庫的選擇性引數： 

- **/ SkuRecommendationDatabasesToRecommend**:要提出建議的資料庫清單。 輸入.csv 中找到的資料庫名稱會區分大小寫，以及必須 (1)、 （2） 每個以雙引號括住和 （3） 每個名稱之間的單一空格來分隔 (例如 /SkuRecommendationDatabasesToRecommend ="Database1""Database2""Database3"). 省略此參數確保建議可供識別輸入的.csv 檔案中的所有使用者資料庫。  

以下是一些範例引動過程：

**範例 1:取得建議與預設的價格。使用離線模式中執行時，或當無法驗證認證。**

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true
```

**範例 2:指定的區域 (例如，"UKWest 」)，取得包含最新價格的建議。**

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationInteractiveAuthentication=true
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
```

**範例 3:（例如取得特定資料庫的建議「 TPCDS1G，EDW_3G，TPCDS10G")。**

```
.\DmaCmd.exe /Action=SkuRecommendation 
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv" 
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv" 
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json" 
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html" 
/SkuRecommendationCurrencyCode=USD 
/SkuRecommendationOfferName=MS-AZR-0044p 
/SkuRecommendationRegionName=UKWest 
/SkuRecommendationSubscriptionId=<Your Subscription Id> 
/SkuRecommendationDatabasesToRecommend=“TPCDS1G” “EDW_3G” “TPCDS10G” 
/AzureAuthenticationInteractiveAuthentication=true 
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId> 
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
```

如需單一資料庫的建議，TSV 輸出檔案會看起來像這樣：

![DMA 資料夾中所示的 PowerShell 單一資料庫檔案](../dma/media/dma-sku-recommend-single-db-recommendations.png)

如需受控執行個體的建議，TSV 輸出檔案會看起來像這樣：

![DMA 資料夾中所示的 PowerShell 受控執行個體檔案](../dma/media/dma-sku-recommend-mi-recommendations.png)

以下的輸出檔中的每個資料行的描述。

- **DatabaseName** -您的資料庫名稱。
- **MetricType** -建議使用 Azure SQL Database 單一資料庫/受控執行個體層。
- **MetricValue** -建議使用 Azure SQL Database 單一資料庫/受控執行個體 SKU。
- **PricePerMonth** – 預估每月相對應的 SKU 價格。
- **RegionName** – 相對應的 SKU 的區域名稱。 
- **IsTierRecommended** -我們提供最小 SKU 建議為每個層。 此外，我們就會套用啟發學習法來判斷適合您的資料庫層。 這會反映資料庫建議哪一層。 
- **ExclusionReasons** -這個值是空白，如果建議的層。 每個層級，不建議，我們會提供為什麼它不挑選的原因。
- **AppliedRules** -簡短的標記法的已套用的規則。

最後一個建議的定價層 (亦即**MetricType**) 和值 (亦即， **MetricValue**)-其中找到**IsTierRecommended**資料行是 TRUE-反映最低 SKU您的查詢，在 Azure 中執行與成功率類似於您的內部部署資料庫的必要項。 對於受管理的執行個體，DMA 目前支援最常用的 8vcore 40vcore sku 的建議。 比方說，如果建議的最低 SKU S4 適用於標準層中，然後選擇 S3 或下方將會導致查詢逾時或無法執行。

HTML 檔案包含以圖形格式的這項資訊。 它提供方便使用方法來檢視最終的建議和佈建程序的下一個部分。 在 HTML 輸出的詳細資訊，是下一節。

## <a name="provision-recommended-skus-to-azure"></a>建議 Azure Sku 佈建

只須點幾下，您可以使用來佈建目標 Sku 中，您可以將資料庫移轉的 Azure 識別出的建議。 您可以使用 HTML 檔案，輸入 Azure 訂用帳戶;挑選定價層、 計算層級和資料大小上限為您的資料庫;與產生的指令碼來佈建您的資料庫。 您可以執行此指令碼，使用 PowerShell。

您可以執行此程序的單一電腦上，或者您可以執行它來判斷 SKU 建議大規模的多部電腦上。 DMA 目前可讓簡單且可調整的體驗支援透過命令列介面的整個程序。

若要輸入佈建資訊並進行變更的建議，更新 HTML 檔案，如下所示。

**如需單一資料庫的建議**

![Azure SQL DB SKU 建議畫面](../dma/media/dma-sku-recommend-single-db-recommendations1.png)

1. 開啟 HTML 檔案，並輸入下列資訊：
    - **訂用帳戶識別碼**-您要佈建資料庫的 Azure 訂用帳戶的訂用帳戶識別碼。
    - **資源群組**-您要將資料庫部署的資源群組。 輸入資源群組存在。
    - **區域**-在其中佈建資料庫的區域。 請確定您的訂用帳戶支援選取的區域。
    - **伺服器名稱**-您要部署之資料庫的 Azure SQL Database 伺服器。 如果您輸入伺服器名稱不存在，就會建立它。
    - **系統管理員使用者名稱**-伺服器管理員使用者名稱。
    - **系統管理員密碼**-伺服器管理員密碼。 密碼必須至少八個字元，長度不得超過 128 個字元。 您的密碼必須包含三個以下類別的字元-英文大寫字母、 英文小寫字母、 數字 (0-9) 和非英數字元 (！、 $、 #、 %等。)。 密碼不能包含全部或部分 （3 + 連續字母） 從使用者名稱。

2. 檢閱每個資料庫的建議和修改的定價層、 計算層級，以及所需的最大的資料大小。 請務必取消選取您目前不想要佈建的任何資料庫。

3. 選取 **產生的佈建指令碼**儲存指令碼，然後在 PowerShell 中執行。

    此程序應該建立您在 HTML 頁面中選取的所有資料庫。

**如需受控執行個體的建議**

![Azure SQL MI SKU 建議畫面](../dma/media/dma-sku-recommend-mi-recommendations1.png)

1. 開啟 HTML 檔案，並輸入下列資訊：
    - **訂用帳戶識別碼**-您要佈建資料庫的 Azure 訂用帳戶的訂用帳戶識別碼。
    - **資源群組**-您要將資料庫部署的資源群組。 輸入資源群組存在。
    - **區域**-在其中佈建資料庫的區域。 請確定您的訂用帳戶支援選取的區域。
    - **執行個體名稱**– Azure SQL 受控執行個體，且您想要將資料庫移轉的執行個體。 執行個體名稱可以包含僅小寫字母、 數字及 '-'，但它無法開頭或結尾 '-' 不得超過 63 個字元。
    - **執行個體系統管理員使用者名稱**– 執行個體的系統管理員使用者名稱。 請確定您登入名稱符合下列需求-它是 SQL 識別碼，和不一般的系統名稱 （例如系統管理員、 系統管理員、 sa、 root、 dbmanager、 loginmanager 等），或內建的資料庫使用者或角色 （像是 dbo、 guest、 public 等等）。 請確定您的名稱不包含空白字元、 Unicode 字元或非英文字母字元，而且它不是以數字或符號開頭。 
    - **執行個體系統管理員密碼**-執行個體系統管理員密碼。 您的密碼必須至少包含 16 個字元，長度不得超過 128 個字元。 您的密碼必須包含三個以下類別的字元-英文大寫字母、 英文小寫字母、 數字 (0-9) 和非英數字元 (！、 $、 #、 %等。)。 密碼不能包含全部或部分 （3 + 連續字母） 從使用者名稱。
    - **Vnet 名稱**– 所在應該佈建受管理的執行個體的 VNet 名稱。 輸入現有的 VNet 名稱。
    - **子網路名稱**– 所在應該佈建受管理的執行個體的子網路名稱。 輸入現有的子網路名稱。

2. 檢閱建議每個執行個體，並修改定價層、 計算層級，以及所需的最大的資料大小。 目前僅限於 40vcore sku 8vcore 建議時，仍有佈建 64vcore 和 80vcore Sku，如有需要的選項。 請務必取消選取任何您目前不想要佈建的執行個體。

    此程序應該建立您在 HTML 頁面中選取的所有資料庫。

    > [!NOTE]
    > 建立子網路上的受管理的執行個體 （特別是針對第一次），可能需要數小時才能完成。 透過 PowerShell 執行佈建指令碼之後，您可以檢查您的部署在 Azure 入口網站上的狀態。

## <a name="next-step"></a>下一步

- 從 CLI 執行 DMA 的命令的完整清單，請參閱文章[執行 Data Migration Assistant 從命令列](https://docs.microsoft.com/sql/dma/dma-commandline?view=sql-server-2017)。
