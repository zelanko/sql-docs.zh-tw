---
title: "設定一般檔案目的地 (SQL Server 匯入和匯出精靈) | Microsoft Docs"
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
  - "sql13.dts.impexpwizard.configureflatfiledest.f1"
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
caps.latest.revision: 53
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# 設定一般檔案目的地 (SQL Server 匯入和匯出精靈)
  如已選取一般檔案目的地，則在指定要複製資料表之後或提供查詢之後，[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [設定一般檔案目的地]。 在此頁面上，您可以指定目的地一般檔案的格式化選項。 (選擇性) 您可以檢閱個別資料行的對應，並預覽範例資料。  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>[設定一般檔案目的地] 頁面的螢幕擷取畫面  
 下列螢幕擷取畫面顯示精靈的 [設定一般檔案目的地] 頁面。
 
 在本例中，使用者想要建立一般的 CSV (逗號分隔值) 檔案，亦即使用歸位/換行字元組合來結束輸出中資料的每個資料列，以及使用逗號分隔每個資料列內資料的資料行。

 ![Configure flat file page of the Import and Export Wizard](../../integration-services/import-export-data/media/flat-file.png "Configure flat file page of the Import and Export Wizard")  
  
## <a name="pick-a-source-table"></a>挑選來源資料表。 
 **來源資料表或檢視表**  
 選取來源資料表或檢視表。  

## <a name="specify-the-row-and-column-delimiters"></a>指定資料列和資料行分隔符號
 **資料列分隔符號**  
 從資料列分隔符號的清單中選取。 沒有任何選項可以指定自訂資料列分隔符號。  
  
|Value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|資料列是使用歸位/換行字元組合進行分隔。|  
|**{CR}**|資料列是使用歸位字元進行分隔。|  
|**{LF}**|資料列是使用換行字元進行分隔。|  
|**分號 {;}**|資料列是使用分號進行分隔。|  
|**冒號 {:}**|資料列是使用冒號進行分隔。|  
|**逗號 {,}**|資料列是使用逗號進行分隔。|  
|**定位字元 {t}**|資料列是使用定位字元進行分隔。|  
|**分隔號 {&#124;}**|資料列是使用分隔號進行分隔。|  
  
 **資料行分隔符號**  
 從資料行分隔符號的清單中選取。 沒有任何選項可以指定自訂資料行分隔符號。  
  
|Value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|資料行是使用歸位/換行字元組合進行分隔。|  
|**{CR}**|資料行是使用歸位字元進行分隔。|  
|**{LF}**|資料行是使用換行字元進行分隔。|  
|**分號 {;}**|資料行是使用分號進行分隔。|  
|**冒號 {:}**|資料行是使用冒號進行分隔。|  
|**逗號 {,}**|資料行是使用逗號進行分隔。|  
|**定位字元 {t}**|資料行是使用定位字元進行分隔。|  
|**分隔號 {&#124;}**|資料行是使用分隔號進行分隔。|  

## <a name="optionally-edit-column-mappings-and-preview-sample-data"></a>選擇性編輯資料行的對應及預覽範例資料

**編輯對應**   
選擇性地按一下 [編輯對應]，顯示所選取資料表的 [資料行對應] 對話方塊。 使用 [資料行對應] 對話方塊即可執行下列動作。
-   檢閱個別資料行在來源與目的地之間的對應。
-   您可以針對不想要複製的資料行選取 [忽略]，只複製資料行的子集。

如需詳細資訊，請參閱[資料行對應](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。  

**預覽**  
在 [預覽資料] 對話方塊中，選擇性地按一下 [預覽] 預覽最多 200 個取樣資料列。 這會確認精靈即將複製您想要複製的資料。 如需詳細資訊，請參閱[預覽資料](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)。  
  
在您預覽資料之後，可能會想要變更已在精靈的先前頁面上選取的選項。 若要進行這些變更，請返回 [設定一般檔案目的地] 頁面，然後按一下 [上一步] 返回先前的頁面，如此您就可以在其中變更選取項目。  

## <a name="whats-next"></a>下一步  
 指定目的地一般檔案的格式化選項之後，下一個頁面是 [Save and Execute Package (儲存和執行封裝)]。 在此頁面上，您可以指定是否要立即執行作業。 根據組態，您也可以儲存精靈所建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，以便在稍後進行自訂並重複使用。 如需詳細資訊，請參閱[儲存和執行封裝](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。  
