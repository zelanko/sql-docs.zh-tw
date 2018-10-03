---
title: 資料行對應 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 790542daa3cf69f5d1cd149a3356545fe69b03e2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47733866"
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>資料行對應 (SQL Server 匯入和匯出精靈)
  選取現有資料表和檢視，以複製或檢視您所提供的查詢之後，如果您按一下 [編輯對應]， [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [資料行對應]  對話方塊。 在此頁面上，您可以指定並設定目的地資料行以接收從來源資料行中複製的資料。 您通常不需要變更此頁面上的任何項目。
  
如果您不想要複製所選取資料表中的所有資料行，則可以在此頁面上執行的動作是排除不想要的資料行。 針對您不想要複製的資料行，在 [對應] 清單的 [目的地] 資料行中選取 [忽略]。
 
## <a name="screen-shot-of-the-column-mappings-page"></a>[資料行對應] 頁面的螢幕擷取畫面 
 下列螢幕擷取畫面顯示精靈的 [資料行對應] 對話方塊範例。 
 
 在此範例中，因為選取了 [建立目的地資料表]  ，所以您會看到精靈即將建立新的目的地資料表。 精靈預設會在新目的地資料表的每個資料行中提供與對應來源資料行相同的名稱、資料類型和屬性。 
  
 ![[匯入和匯出精靈] 的 [資料行對應] 頁面](../../integration-services/import-export-data/media/column-mappings.png "[匯入和匯出精靈] 的 [資料行對應] 頁面")  
  
## <a name="review-the-source-and-destination"></a>檢閱來源和目的地 
![資料行對應頁面、來源和目的地區段](../../integration-services/import-export-data/media/column-mappings-page-source-and-destination-section.png)

 **Source**  
 選取的來源資料表、檢視或查詢。  
  
 **目的地**  
 選取的目的地資料表或檢視。  

## <a name="optionally-create-a-new-destination-table"></a>選擇性地建立新的目的地資料表
![資料行對應頁面、新增資料表區段](../../integration-services/import-export-data/media/column-mappings-page-new-table-section.png)

 **建立目的地資料表/檔案**  
 如果還沒有目的地資料表，則請建立目的地資料表。    
  
 **編輯 SQL**  
按一下 [編輯 SQL]  以開啟 [建立資料表的 SQL 陳述式]  對話方塊。 使用自動產生的 CREATE TABLE 陳述式，或依您的用途進行修改。 如果您手動變更此陳述式，您必須確定資料行對應清單能夠辨識您所做的變更。 如需詳細資訊，請參閱 [Create Table SQL Statement](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)(建立資料表的 SQL 陳述式)。  

### <a name="sometimes-these-options-are-disabled"></a>有時會停用這些選項
自動啟用或自動停用 [建立目的地資料表/檔案] 選項和 [編輯 SQL] 按鈕。

-   **已啟用。** 如果您已在 [選取來源資料表和檢視] 頁面上指定**新**目的地資料表，就會自動選取 [建立目的地資料表] 選項，並且會啟用 [編輯 SQL] 按鈕。

-   **已停用。** 如果您已在 [選取來源資料表和檢視] 頁面上選取**現有**目的地資料表，就會停用 [建立目的地資料表] 選項和 [編輯 SQL] 按鈕。 如果您想要建立新的目的地資料表，請移回 [選取來源資料表和檢視] 頁面，並在 [目的地] 資料行中輸入**新**資料表的名稱。  

## <a name="what-about-existing-data-in-the-destination"></a>目的地中的現有資料如何？
![資料行對應頁面、選項區段](../../integration-services/import-export-data/media/column-mappings-page-options-section.png)

 **刪除目的地資料表/檔案中的資料列**  
 指定在載入新資料之前，是否要清除現有資料表中的資料。  
  
 **將資料列附加至目的地資料表/檔案**  
 指定是否要將新資料附加到現有資料表中已存在的資料後面。  
  
 **卸除並重新建立目的地資料表**  
 選擇此選項即可覆寫目的地資料表。 只有在您使用精靈來建立目的地資料表時，才能使用這個選項。 目的地資料表只有在您儲存精靈所建立的套件，然後再次執行套件時才會卸除並重建。 當您想要多次測試設定時，這是一個很方便的選項。
  
 **啟用識別插入**  
 選擇此選項即可允許將來源資料中的現有識別值，插入目的地資料表裡的識別欄位中。 依預設，目的地識別欄位並不允許此動作。  
  
> [!TIP]
> 如果您現有的主索引鍵位於識別資料行、autonumber 資料行或對等項目內，您通常必須選取此選項來保留現有的主索引鍵值。  否則目的地識別欄位通常會指派新值。  

## <a name="keep-your-autonumber-or-identity-values"></a>保留自動編號或識別值
如果您正在匯出的資料具有自動編號資料行或識別資料行 (例如，如果您是要從 Microsoft Access 匯出)，請確定您選取 [啟用識別插入]，如上所述。

## <a name="review-column-mappings"></a>檢閱資料行對應
![資料行對應頁面、對應區段](../../integration-services/import-export-data/media/column-mappings-page-mappings-section.png)

 **對應**  
 顯示資料來源中的每個資料行如何對應至目的地中的資料行。
 
這份 **對應** 清單具有下列資料行。  
  
-    **Source**  
     檢視每個來源資料行。  
  
-   **目的地**  
    檢視對應的目的地資料行，或選取不同的資料行。
    
    您不需要複製來源資料表中的所有資料行。 針對您想要跳過的資料行，選取此資料行中的 [忽略]。 在對應資料行之前，您必須忽略不會加以對應的所有資料行。  
  
-   **型別**  
    檢視目的地資料行的資料類型，或選取不同的資料類型。
  
-   **可為 Null**  
    指定目的地資料行是否允許 Null 值。  
  
-   **大小**  
    指定目的地資料行中的字元數 (如適用)。  
  
-    **有效位數**  
    指定目的地資料行中數值資料的整數位數，即數字的位數 (適用時)。  
  
 -   **小數位數**  
    指定目的地資料行中數值資料的小數位數，即小數位數 (適用時)。  
  
## <a name="whats-next"></a>下一步  
 檢閱並設定目的地資料行以接收從來源資料行複製的資料，且按一下 [確定] 之後，[資料行對應] 對話方塊會將您返回 [選取來源資料表和檢視] 頁面或 [設定一般檔案目的地] 頁面。 如需詳細資訊，請參閱 [選取來源資料表和檢視](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) 或 [設定一般檔案目的地](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)。  
  
 如果指定一個可能會在 [對應]  清單中失敗的對應，則 [資料行對應]  對話方塊會將您導向至 [檢閱資料類型對應]  頁面。 在此頁面上，您可以檢閱警告，指定轉換選項，同時指定如何處理錯誤。 如需詳細資訊，請參閱 [檢閱資料類型對應](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)。  
 
 ## <a name="see-also"></a>另請參閱
[SQL Server 匯入及匯出精靈的資料類型對應](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)  
[透過匯入和匯出精靈的簡單範例開始使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

