---
title: "資料行對應 (SQL Server 匯入和匯出精靈) | Microsoft Docs"
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
  - "sql13.dts.impexpwizard.columnmapandtransform.f1"
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
caps.latest.revision: 69
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# 資料行對應 (SQL Server 匯入和匯出精靈)
  選取現有資料表和檢視，以複製或檢視您所提供的查詢之後，如果您按一下 [編輯對應]，[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [資料行對應] 對話方塊。 您可以在此頁面上指定並設定要接收複製資料的目的地資料行。  
 
## <a name="screen-shot-of-the-column-mappings-page"></a>[資料行對應] 頁面的螢幕擷取畫面 
 下列螢幕擷取畫面顯示精靈的 [資料行對應] 對話方塊。 
 
 在此範例中，因為選取了 [建立目的地資料表]，所以您會看到精靈即將建立新的目的地資料表。 依預設，新的目的地資料表中的每個資料行都會和對應來源資料行具有相同的名稱、資料類型和屬性。 
  
 ![Column mappings page of the Import and Export Wizard](../../integration-services/import-export-data/media/column-mappings.png "Column mappings page of the Import and Export Wizard")  
  
## <a name="confirm-the-source-and-destination"></a>確認來源與目的地  
 **來源**  
 識別選取的來源資料表、檢視，或查詢。  
  
 **目的地**  
 識別選取的目的地資料表或檢視表。  

## <a name="create-a-new-destination-table"></a>建立新的目的地資料表
 **建立目的地資料表/檔案**  
 如果沒有，就請建立目的地資料表。    
  
 **編輯 SQL**  
按一下 [編輯 SQL] 以開啟 [建立資料表的 SQL 陳述式] 對話方塊。 使用預設的 CREATE TABLE 陳述式，或依您的用途修改。 如果您手動變更此陳述式，您必須確定資料行對應清單能夠辨識您所做的變更。 如需詳細資訊，請參閱 [Create Table SQL Statement](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md) (建立資料表的 SQL 陳述式)。  
  
 > [!TIP] 如果您指定 [選取來源資料表和檢視] 頁面上的新目的地資料表，就會自動選取 [建立目的地資料表] 選項，並且會啟用 [編輯 SQL] 按鈕。 否則，如果您想要建立目的地資料表，您必須移回至 [選取來源資料表和檢視] 頁面上，並在 [目的地] 資料行中輸入**新**資料表的名稱。
>
> 如果 [建立目的地資料表] 選項和 [編輯 SQL] 上按鈕已在 [資料行對應] 頁面上停用，請回到 [選取來源資料表和檢視] 頁面並輸入 [目的地] 資料行中**新**資料表的名稱。 指定一或多個新的目的地資料表，並按一下 [下一步]會自動選取 [建立目的地資料表] 選項，而且會在 [資料行對應] 頁面上啟用 [編輯 SQL] 按鈕。 選取 [編輯 SQL] 以顯示 [建立資料表的 SQL 陳述式] 對話方塊。  

## <a name="specify-options-for-existing-data-in-the-destination"></a>為目的地中的現有資料指定選項
 **刪除目的地資料表/檔案中的資料列**  
 指定在載入新資料之前，是否要清除現有資料表中的資料。  
  
 **將資料列附加至目的地資料表/檔案**  
 指定是否要將新資料附加到現有資料表中已存在的資料後面。  
  
 **卸除並重新建立目的地資料表**  
 選擇此選項即可覆寫目的地資料表。 只有在您使用精靈來建立目的地資料表時，才能使用這個選項。 目的地資料表只有在您儲存精靈所建立的套件，然後再次執行套件時才會卸除並重建。 當您想要多次測試設定時，這是一個很方便的選項。
  
 **啟用識別插入**  
 選擇此選項即可允許將來源資料中的現有識別值，插入目的地資料表裡的識別欄位中。 依預設，目的地識別欄位並不允許此動作。  
  
> [!TIP] 如果您現有的主索引鍵位於識別資料行、autonumber 資料行或對等項目內，您通常必須選取此選項來保留現有的主索引鍵值。  否則目的地識別欄位通常會指派新值。  

## <a name="review-column-mappings-and-destination-data-types"></a>檢閱資料行對應與目的地資料類型 
 **對應**  
 顯示資料來源中的每個資料行如何對應至目的地中的資料行。
 
 針對複製不想要的資料行，在 [目的地] 資料行中選取 [忽略]。 您不必複製資料表中的所有資料行。  
 
 ![資料行對應 - 對應](../../integration-services/import-export-data/media/column-mappings-mappings.png)
  
 這份**對應**清單具有下列資料行。  
  
-    **來源**  
     檢視每個來源資料行，如有必要，您可以指定轉換設定。  
  
-   **目的地**  
    檢視對應的目的地資料行，或選取不同的資料行。
    
    指定在進行複製作業的期間，您是否想要忽略某資料行。 您可以針對要略過的資料行，在此資料行中選取 [忽略]，只複製資料行的子集。 在對應資料行之前，您必須忽略不會加以對應的所有資料行。  
  
-   **類型**  
    檢視目的地資料行的資料類型，或選取不同的資料類型。
  
-   **可為 Null**  
    指定目的地資料行是否允許 Null 值。  
  
-   **大小**  
    指定目的地資料行中的字元數 (如適用)。  
  
-    **有效位數**  
    指定目的地資料行中數值資料的整數位數，這裡指的是數字的位數 (如適用)。  
  
 -   **小數位數**  
    指定目的地資料行中數值資料的小數位數，這裡指的是小數位數 (如適用)。  
  
## <a name="whats-next"></a>下一步  
 指定並設定接收複製資料的目的地資料行，且按一下 [確定] 之後，[資料行對應] 對話方塊會將您傳回至 [選取來源資料表和檢視] 頁面或 [設定一般檔案目的地] 頁面。 如需詳細資訊，請參閱[選取來源資料表和檢視](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)或[設定一般檔案目的地](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)。  
  
 如果指定一個可能會在 [對應] 清單中失敗的對應，則 [資料行對應] 對話方塊會將您導向至 [檢閱資料類型對應] 頁面。 在此頁面上，您可以檢閱警告，指定轉換選項，同時指定如何處理錯誤。 如需詳細資訊，請參閱[檢閱資料類型對應](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)。  
 
 ## <a name="see-also"></a>另請參閱
[SQL Server 匯入及匯出精靈的資料類型對應](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
