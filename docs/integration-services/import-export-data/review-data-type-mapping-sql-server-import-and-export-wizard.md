---
title: "檢閱資料類型對應 (SQL Server 匯入和匯出精靈) | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.reviewissues.f1"
ms.assetid: 0625c4f9-b8ff-4593-b884-39398b9d43af
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# 檢閱資料類型對應 (SQL Server 匯入和匯出精靈)
如果您所指定的資料類型對應在 [資料行對應] 對話方塊的 [對應] 清單中失敗，則 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [檢閱資料類型對應] 頁面。 在這個頁面上，您可以檢閱精靈必須執行才能讓來源資料與目的地相容之資料類型轉換的詳細資訊。 這項資訊包括視覺提示，可區別預期會成功的轉換與可能導致錯誤或截斷的轉換。 針對每個轉換，您可以決定是否要接受精靈所建議的轉換，而且可以指定如何處理發生的任何錯誤。   
  
如需精靈如何對應來源資料行和目的地資料行之間的資料類型資訊，請參閱[精靈如何對應來源和目的地之間的資料類型](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardMapping)。

> [!TIP] 您無法在 [檢閱資料類型對應] 頁面上變更資料類型對應。 不過，您可以按一下 [上一步] 返回 [選取來源資料表和檢視表] 頁面，然後按一下 [編輯對應] 再次開啟 [資料行對應] 對話方塊。 在 [資料行對應] 對話方塊中，您可以指定較可能成功的資料類型對應。 若要再次查看 [資料行對應] 對話方塊，請參閱[資料行對應](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。  
  
## <a name="screen-shot-of-the-review-data-type-mapping-page"></a>[檢閱資料類型對應] 頁面的螢幕擷取畫面
 下列螢幕擷取畫面會在使用者所指定的對應在 [資料行對應] 對話方塊中可能失敗之後，顯示精靈的 [檢閱資料類型對應] 頁面。
 
 在此範例中：
 -   [資料表] 清單中資料列上的警告圖示，指出將至少一個資料行從查詢結果轉換成目的地資料表中的相容資料類型時發生問題。
 -   [資料類型對應] 清單中第一個資料行上的警告圖示，指出從來源資料行的 **int** 資料類型對應至目的地資料行的 **smalldatetime** 資料類型可能會導致資料遺失。
 
 ![Review Data Type Mapping page of the Import and Export Wizard](../../integration-services/import-export-data/media/review-mapping.png "Review Data Type Mapping page of the Import and Export Wizard") 
 
## <a name="review-the-source-and-destination-tables"></a>檢閱來源與目的地資料表  
 [檢閱資料類型對應] 頁面的上半部是 [資料表] 清單，其中列出要從來源複製至目的地的資料表。 若要查看個別資料表的轉換資訊，請在 [資料表] 清單中選取資料表。 所選取資料表之資料行的轉換資訊會顯示在此頁面下半部的 [資料類型對應] 方格中。
 
![檢閱對應 - 資料表](../../integration-services/import-export-data/media/review-mapping-tables.png)
  
 下表描述 [資料表] 清單中的資料行。  
  
|資料行|說明|  
|------------|-----------------|  
|來源圖示|指出資料類型轉換的成功機率：<br /> -   **綠色**的核取記號圖示表示精靈預期這個資料表的所有資料類型轉換都會成功。<br />-   **黃色**的警告圖示表示您應該檢閱精靈即將執行的個別轉換。 若要檢閱這些轉換，請選取資料表，然後在 **[資料類型對應]** 清單中檢閱個別資料行的轉換。<br />-   **紅色**的錯誤圖示表示精靈無法確實針對這個資料表執行某些轉換。|  
|**來源**|來源資料表的名稱。|  
|目的地圖示|指出目的地已經存在或將由精靈建立：<br /> -   資料表圖示表示目的地是現有的資料表。<br />-   含有光環的資料表圖示表示目的地是精靈即將建立的新資料表。|  
|**目的地**|目的地資料表的名稱。|  
  
## <a name="review-the-data-type-mappings-from-source-to-destination"></a>檢閱從來源到目的地的資料類型對應  
 [檢閱資料類型對應] 頁面的下半部是 [資料類型對應] 清單。 此方格會提供有關在 **[資料表]** 清單中選取之資料表內資料行的詳細轉換資訊。
 
![檢閱對應 - 對應](../../integration-services/import-export-data/media/review-mapping-mappings.png)  

下表描述 [資料類型對應] 清單中的資料行。 

|資料行|說明|  
|------------|-----------------|  
|轉換圖示|指出資料類型轉換的成功機率：<br /> -   **綠色**的核取記號圖示表示精靈預期這個資料行的資料類型轉換會成功。<br />-   **黃色**的警告圖示表示您應該檢閱精靈即將執行的轉換。 若要檢閱轉換，請按兩下資料行，即可檢視 [資料行轉換詳細資訊] 對話方塊。 如需詳細資訊，請參閱[資料行轉換詳細資訊對話方塊](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)。<br />-   **紅色**錯誤圖示表示精靈無法確實執行轉換。|  
|**來源資料行**|來源資料行的名稱。|  
|**來源類型**|來源資料行的資料類型。|  
|**目的地資料行**|目的地資料行的名稱。|  
|**目的地類型**|目的地資料行的資料類型。|  
|**轉換**|指定是否繼續規劃的轉換：<br /> -   選取此核取方塊，即可讓精靈繼續進行規劃的轉換。<br />-   清除此核取方塊，即可取消資料類型轉換。|  
|**錯誤時**|指定精靈如何處理錯誤：<br /> -   使用 [錯誤時 (全域)] 設定，您可以在此頁面底部指定該設定。<br />-   因錯誤而失敗，並停止匯入或匯出程序。<br />-   忽略錯誤。|  
|**截斷時**|指定精靈如何處理截斷：<br /> -   使用 [截斷時 (全域)] 設定，您可以在此頁面底部指定該設定。<br />-   因錯誤而失敗，並停止匯入或匯出程序。<br />-   忽略截斷。|  

> [!TIP] 若要查看特定資料行轉換的詳細資訊，請在清單中按兩下任何資料列。 此時， **[資料行轉換詳細資訊]** 對話方塊會開啟並針對該資料行顯示更詳細的轉換資訊。 如需詳細資訊，請參閱[資料行轉換詳細資訊對話方塊](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)。
 
## <a name="specify-global-error-handling-options"></a>指定全域錯誤處理選項  
 [檢閱資料類型對應] 頁面的下半部可讓您指定預設會套用至所有資料行的錯誤處理選項。 這些設定會套用在 [資料類型對應] 清單的 [錯誤時] 或 [截斷時] 資料行中選取了 [使用全域] 的所有轉換。   
 
![檢閱對應 - 錯誤](../../integration-services/import-export-data/media/review-mapping-errors.png)

 **錯誤時 (全域)**  
 指定精靈如何處理錯誤：  
 -   因錯誤而失敗，並停止匯入或匯出程序。  
 -   忽略錯誤，並繼續進行匯入或匯出程序。  
  
 **截斷時 (全域)**  
 指定精靈如何處理資料截斷：  
 -   因錯誤而失敗，並停止匯入或匯出程序。  
 -   忽略截斷，並繼續進行匯入或匯出程序。  
   
## <a name="whats-next"></a>下一步  
 檢閱警告、指定轉換選項，並指定如何處理錯誤之後，[檢閱資料類型對應] 頁面會將您帶回 [資料行對應] 對話方塊。 如需詳細資訊，請參閱[資料行對應](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。  
