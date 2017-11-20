---
title: "資料行對應 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b1ed879f21396c3c8d588307eaf087daea8c44c3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>資料行對應 (SQL Server 匯入和匯出精靈)
  選取現有資料表和檢視，以複製或檢視您所提供的查詢之後，如果您按一下 [編輯對應]， [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [資料行對應]  對話方塊。 此頁面上您可以指定並設定要接收資料從來源資料行複製目的地資料行。 通常，您不必變更此頁面上的任何項目。
  
如果您不想複製您所選取的資料表中的所有資料行，您可以在此頁面上的一件事是排除不要的資料行。 選取**忽略**中**目的地**資料行**對應**不想要複製的資料行的清單。
 
## <a name="screen-shot-of-the-column-mappings-page"></a>[資料行對應] 頁面的螢幕擷取畫面 
 下列螢幕擷取畫面顯示的範例**資料行對應**精靈對話方塊。 
 
 在此範例中，因為選取了 [建立目的地資料表]  ，所以您會看到精靈即將建立新的目的地資料表。 根據預設，精靈會讓每個新的目的地資料表相同的名稱中的資料行、 資料類型和屬性對應的來源資料行。 
  
 ![資料行對應 頁面的匯入和匯出精靈](../../integration-services/import-export-data/media/column-mappings.png "匯入和匯出精靈 」 的資料行對應 頁面")  
  
## <a name="review-the-source-and-destination"></a>檢閱來源和目的地 
![資料行對應 頁面、 來源和目的地 > 一節](../../integration-services/import-export-data/media/column-mappings-page-source-and-destination-section.png)

 **Source**  
 所選的來源資料表、 檢視或查詢中。  
  
 **目的地**  
 選取的目的地資料表或檢視。  

## <a name="optionally-create-a-new-destination-table"></a>（選擇性） 建立新的目的地資料表
![資料行對應 頁面上新的資料表區段](../../integration-services/import-export-data/media/column-mappings-page-new-table-section.png)

 **建立目的地資料表/檔案**  
 如果不存在，請建立目的地資料表。    
  
 **編輯 SQL**  
按一下 [編輯 SQL]  以開啟 [建立資料表的 SQL 陳述式]  對話方塊。 使用自動產生 CREATE TABLE 陳述式，或修改您的目的。 如果您手動變更此陳述式，您必須確定資料行對應清單能夠辨識您所做的變更。 如需詳細資訊，請參閱 [Create Table SQL Statement](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)(建立資料表的 SQL 陳述式)。  

### <a name="sometimes-these-options-are-disabled"></a>有時候停用這些選項
**建立目的地資料表/檔案**選項和**編輯 SQL**按鈕自動啟用或自動停用。

-   **啟用。** 如果您指定**新**目的地資料表上的**選取來源資料表和檢視** 頁面上，**建立目的資料表**選項會自動選取和**編輯 SQL**按鈕啟用。

-   **已停用。** 如果您選取**現有**目的地資料表上的**選取來源資料表和檢視** 頁面上，**建立目的資料表**選項和**編輯 SQL**按鈕已停用。 如果您想要建立新的目的地資料表，請回到**選取來源資料表和檢視**頁面上，輸入名稱**新**資料表中**目的地**資料行。  

## <a name="what-about-existing-data-in-the-destination"></a>目的地中的現有資料呢？
![資料行對應 頁面上選項 > 一節](../../integration-services/import-export-data/media/column-mappings-page-options-section.png)

 **刪除目的地資料表/檔案中的資料列**  
 指定在載入新資料之前，是否要清除現有資料表中的資料。  
  
 **將資料列附加至目的地資料表/檔案**  
 指定是否要將新資料附加到現有資料表中已存在的資料後面。  
  
 **卸除並重新建立目的地資料表**  
 選擇此選項即可覆寫目的地資料表。 當您使用精靈來建立目的地資料表時，才可用這個選項。 目的地資料表只有在您儲存精靈所建立的套件，然後再次執行套件時才會卸除並重建。 當您想要多次測試設定時，這是一個很方便的選項。
  
 **啟用識別插入**  
 選擇此選項即可允許將來源資料中的現有識別值，插入目的地資料表裡的識別欄位中。 依預設，目的地識別欄位並不允許此動作。  
  
> [!TIP]
> 如果您現有的主索引鍵位於識別資料行、autonumber 資料行或對等項目內，您通常必須選取此選項來保留現有的主索引鍵值。  否則目的地識別欄位通常會指派新值。  

## <a name="keep-your-autonumber-or-identity-values"></a>保留自動編號或身分識別的值
如果您正在匯出具有 autonumber 資料行或識別資料行的資料，例如，如果您要匯出從 Microsoft Access-請確定選取**啟用識別插入**如立即上面所述。

## <a name="review-column-mappings"></a>檢閱資料行對應
![資料行對應 頁面上的對應區段](../../integration-services/import-export-data/media/column-mappings-page-mappings-section.png)

 **對應**  
 顯示資料來源中的每個資料行如何對應至目的地中的資料行。
 
這份 **對應** 清單具有下列資料行。  
  
-    **Source**  
     檢視每個來源資料行。  
  
-   **目的地**  
    檢視對應的目的地資料行，或選取不同的資料行。
    
    您不需要從來源資料表中複製所有資料行。 選取**忽略**中此資料行，您想略過的資料行。 在對應資料行之前，您必須忽略不會加以對應的所有資料行。  
  
-   **類型**  
    檢視目的地資料行的資料類型，或選取不同的資料類型。
  
-   **可為 Null**  
    指定目的地資料行是否允許 Null 值。  
  
-   **大小**  
    指定目的地資料行中的字元數 (如適用)。  
  
-    **有效位數**  
    如果適用的話，請在目的地資料行-也就是數字的數目-中指定數值資料的有效的位數。  
  
 -   **小數位數**  
    如果適用的話，請在目的地資料行-也就是小數位數的數目-中指定的小數位數字資料。  
  
## <a name="whats-next"></a>下一步  
 在檢閱和設定目的地資料行接收複製從來源資料行的資料，然後按一下**確定**、**資料行對應**對話方塊會傳回您**選取來源資料表和檢視表**頁面上，或者**設定一般檔案目的地**頁面。 如需詳細資訊，請參閱 [選取來源資料表和檢視](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) 或 [設定一般檔案目的地](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)。  
  
 如果指定一個可能會在 [對應]  清單中失敗的對應，則 [資料行對應]  對話方塊會將您導向至 [檢閱資料類型對應]  頁面。 在此頁面上，您可以檢閱警告，指定轉換選項，同時指定如何處理錯誤。 如需詳細資訊，請參閱 [檢閱資料類型對應](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)。  
 
 ## <a name="see-also"></a>另請參閱
[SQL Server 匯入及匯出精靈的資料類型對應](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)  
[透過匯入和匯出精靈的簡單範例開始使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


