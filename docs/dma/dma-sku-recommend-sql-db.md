---
title: 識別您的內部部署資料庫 (Data Migration Assistant) 正確的 Azure SQL 資料庫 SKU |Microsoft Docs
description: 了解如何使用 Data Migration Assistant，以識別您的內部部署資料庫權限的 Azure SQL 資料庫 SKU
ms.custom: ''
ms.date: 08/29/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 415de36195960c1a2fa60d3e5dd68168682028e0
ms.sourcegitcommit: fb269accc3786715c78f8b6e2ec38783a6eb63e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2018
ms.locfileid: "43152829"
---
# <a name="identify-the-right-azure-sql-database-sku-for-your-on-premises-database"></a>識別您的內部部署資料庫正確的 Azure SQL 資料庫 SKU

將資料庫移轉至雲端的工作是複雜且耗時，涉及數個變數。 挑選正確的 Azure 資料庫目標和 SKU，您的資料庫可能具有挑戰性。 我們的目標與 Database Migration Assistant (DMA) 是為了解決這些問題，並讓資料庫的移轉體驗，簡單且有效。

本文主要著重於 DMA 的 Azure SQL 資料庫 SKU 建議功能，可讓您找出建議從裝載資料庫的電腦收集效能計數器為基礎的 Azure SQL 資料庫 SKU 的最小。 這項功能提供定價層、 計算層級，和最大的資料大小，以及每月預估的成本的相關建議。 它也提供佈建所有資料庫到 Azure 中大量的能力。

> [!NOTE] 
> 才提供此功能目前只能透過命令列介面 (CLI)。 近期版本中，會新增這項功能透過 DMA 的使用者介面的支援。

下列指示將協助您判斷 Azure SQL 資料庫 SKU 建議，並使用 Data Migration Assistant 佈建至 Azure，相關聯的資料庫。

## <a name="prerequisites"></a>先決條件

下載資料庫移轉小幫手 v4.0 或更新版本，然後再進行安裝。 如果您已經有此工具安裝，請關閉並重新開啟它，並將提示您升級的工具。

## <a name="collect-performance-counters"></a>收集效能計數器

此程序的第一個步驟是收集效能計數器，為您的資料庫。 您可以裝載您資料庫的電腦上執行 PowerShell 命令，以收集效能計數器。 DMA 會將您提供一份此 PowerShell 檔案，但是您也可以使用您自己的方法，以從您的電腦擷取效能計數器。

您不需要個別執行每個資料庫的這項工作。 從電腦收集的效能計數器可用來建議的電腦上主控的所有資料庫的 SKU。

> [!IMPORTANT]
> 執行此命令的電腦需要裝載您資料庫的電腦的系統管理員權限。

1. 確認收集效能計數器所需的 PowerShell 檔案已安裝的 DMA 資料夾中。

    ![DMA 資料夾中所示的 PowerShell 檔案](../dma/media/dma-sku-recommend-data-collection-file.png)

2. 執行 PowerShell 指令碼的下列引數：
    - **ComputerName**： 裝載資料庫之電腦的名稱。
    - **OutputFilePath**： 輸出檔案路徑來儲存所收集的計數器。
    - **CollectionTimeInSeconds**： 在這期間您想要收集效能計數器資料的時間量。
      擷取效能計數器，以取得有意義的建議至少 40 分鐘。 擷取的持續時間越長越精準建議會。
    - **DbConnectionString**： 指向您要從中收集效能計數器資料的電腦上主控的 master 資料庫的連接字串。
     
    以下是範例引動過程：

    ```
    .\SkuRecommendationDataCollectionScript.ps1
     -ComputerName Foobar1
     -OutputFilePath D:\counters2.csv
     -CollectionTimeInSeconds 10
     -DbConnectionString "Server=localhost;Initial Catalog=master;Integrated Security=SSPI;"
    ```
    
    命令執行之後，處理程序會輸出具有您指定的位置中的效能計數器的檔案。 這個檔案可以作為 SKU 建議命令，在下一節中的輸入。

## <a name="use-the-dma-cli-to-get-sku-recommendations"></a>使用 DMA CLI 取得 SKU 建議

使用效能計數器從上一個步驟的輸出檔做為輸入，在此步驟。 DMA 會為您提供 Azure SQL Database 的建議定價層、 計算層級和資料大小上限為每個資料庫在您的電腦上。 DMA 也會提供您估計每月成本為每個資料庫。

使用下列引數執行 dmacmd.exe:

- **/ 動作 = SkuRecommendation**： 輸入此引數執行 SKU 評量。
- **/ SkuRecommendationInputDataFilePath**： 上一節中所收集的計數器檔案的路徑。
- **/ SkuRecommendationTsvOutputResultsFilePath**： 要寫入輸出結果以 TSV 格式的路徑。
- **/ SkuRecommendationJsonOutputResultsFilePath**： 要寫入輸出結果以 JSON 格式的路徑。
- **/ SkuRecommendationHtmlResultsFilePath**： 以 HTML 格式寫入輸出結果的路徑。

此外，您需要挑選其中一個下列的引數：
- 防止價格重新整理
    - **/ SkuRecommendationPreventPriceRefresh**： 發生時，防止價格重新整理。 如果在離線模式中執行，請使用。
- 取得最新的價格 
    - **/ SkuRecommendationCurrencyCode**： 要顯示的價格 （例如貨幣「 USD")。
    - **/ SkuRecommendationOfferName**： 供應項目名稱 （例如："MS-AZR-0003 P")。 如需詳細資訊，請參閱 < [Microsoft Azure 優惠詳細資料](https://azure.microsoft.com/support/legal/offer-details/)頁面。
    - **/ SkuRecommendationRegionName**: 區域名稱 （例如：「 美國西部 」）。
    - **/ SkuRecommendationSubscriptionId**： 訂用帳戶識別碼。
    - **/ AzureAuthenticationTenantId**： 驗證租用戶。
    - **/ AzureAuthenticationClientId**： 用於驗證的 AAD 應用程式的用戶端識別碼。
    - 其中一個下列的驗證選項：
        - 互動式
            - **AzureAuthenticationInteractiveAuthentication**： 設為 true，驗證快顯視窗。
        - 憑證為基礎
            - **AzureAuthenticationCertificateStoreLocation**： 設定憑證存放區位置 （例如：「 CurrentUser")。
            - **AzureAuthenticationCertificateThumbprint**： 設為 憑證指紋。
        - 基礎語彙基元
            - **AzureAuthenticationToken**： 設為憑證的權杖。

以下是一些範例引動過程：

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

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true
```

TSV 輸出檔案包含資料行，如下圖所示：

   ![DMA 資料夾中所示的 PowerShell 檔案](../dma/media/dma-tsv-file-column.png)

遵循每個資料行的描述。

- **DatabaseName** – 您的資料庫名稱。
- **MetricName** – 是否已執行計量。
- **MetricType** -建議使用 Azure SQL Database 層。
- **MetricValue** -建議使用 Azure SQL Database 的 SKU。
- **SQLMiEquivalentCores** -如果您選擇 Azure SQL Database 受控執行個體，您可以使用此值的核心計數。
- **IsTierRecommended** -我們提供最小 SKU 建議為每個層。 此外，我們就會套用啟發學習法來判斷適合您的資料庫層。 
- **ExclusionReasons** -這個值是空白，如果建議的層。 建議您不要每個層，我們會提供為什麼它未選取的原因。
- **AppliedRules** -簡短的標記法的已套用的規則。

請注意，建議的值與成功率類似於您的內部部署資料庫，在 Azure 中執行查詢所需的最低 SKU。 比方說，如果建議的最低 SKU S4 適用於標準層中，然後選擇 S3 或下方將會導致查詢逾時或無法執行。

HTML 檔案包含以圖形格式的這項資訊。 您可以使用 HTML 檔案，輸入 Azure 訂用帳戶資訊、 挑選定價層、 計算層級和資料大小上限為您的資料庫，以及產生指令碼來佈建您的資料庫。 您可以使用 PowerShell 執行此指令碼。

## <a name="provision-your-databases-to-azure"></a>佈建您的 Azure 資料庫
只須點幾下，您可以使用從上一個步驟的建議，以佈建目標資料庫中，您可以將資料庫移轉的 Azure。 您也可以更新 HTML 檔案，如下所示，來進行的建議的變更。

1. 開啟 HTML 檔案，並輸入下列資訊：
    - **訂用帳戶識別碼**– 您要佈建資料庫的 Azure 訂用帳戶的訂用帳戶識別碼。
    - **區域**– 在其中佈建資料庫的區域。 請確定您的訂用帳戶支援選取的區域。
    - **資源群組**– 您要將資料庫部署的資源群組。 輸入資源群組存在。
    - **伺服器名稱**– 您要部署之資料庫的 Azure SQL Database 伺服器。 如果您輸入伺服器名稱不存在，就會建立它。
    - **系統管理員使用者名稱 \ 密碼**-伺服器管理員使用者名稱和密碼。

2. 檢閱每個資料庫的建議和修改的定價層、 計算層級，以及所需的最大的資料大小。 請務必取消選取您目前不想要佈建的任何資料庫。

3. 選取 **產生的佈建指令碼**儲存指令碼，然後在 PowerShell 中執行。

    此程序應該建立您在 HTML 頁面中選取的所有資料庫。

您可以在此程序，在單一電腦上執行的所有步驟，或在您可以判斷 SKU 建議大規模的多部電腦上都執行。 DMA 可讓簡單且可調整的體驗支援透過命令列介面的所有這些步驟。 同樣地，支援透過 DMA 的使用者介面的這項功能可於本年度稍後。

## <a name="next-steps"></a>後續步驟
- 下載最新版[Data Migration Assistant](https://aka.ms/get-dma)。
- 請參閱文章[執行 Data Migration Assistant 從命令列](https://docs.microsoft.com/sql/dma/dma-commandline?view=sql-server-2017)如命令從 CLI 執行 DMA 的完整清單。
