---
title: "設定一般檔案目的地 (SQL Server 的匯入及匯出精靈) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
caps.latest.revision: "53"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e312251291cbf2e8850b7900793b8d32e7c3d53b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>設定一般檔案目的地 (SQL Server 的匯入及匯出精靈)
  若已選取一般檔案目的地，則在指定要複製整個資料表或提供查詢之後，[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入及匯出精靈] 會顯示 [設定一般檔案目的地]。 在此頁面上，您可以指定目的地一般檔案的格式化選項。 (選擇性) 您可以檢閱個別資料行的對應，並預覽範例資料。  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>[設定一般檔案目的地] 頁面的螢幕擷取畫面  
 下列螢幕擷取畫面顯示精靈的 [設定一般檔案目的地] 頁面。
 
 在此範例中，用者指定了下列選項，以建立一般的 CSV (逗號分隔值) 檔案。
-   **資料列分隔符號**。 每個輸出的資料列結尾都會有一組歸位換行與換行字元組合。
-   **資料行分隔符號**。 每一個資料列中的資料行中皆以逗號分隔。

 ![[匯入及匯出精靈] 的 [設定一般檔案] 頁面](../../integration-services/import-export-data/media/flat-file.png)
  
## <a name="pick-a-source-table"></a>挑選來源資料表
 **來源資料表或檢視表**  
-   若在上一頁中指定您要複製資料表，請從下拉式清單中選取來源資料表或檢視。
-   如有提供查詢，會選取唯一的選項 `"Query"`。  

## <a name="specify-row-and-column-delimiters-for-the-output"></a>指定輸出之資料列與資料行的分隔符號
 **資料列分隔符號**  
 從分隔符號清單中選取分隔符號，以分隔輸出中的資料列。 沒有選項可用於指定*自訂*的資料列分隔符號。  
  
|值|說明|  
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
 從分隔符號清單中選取分隔符號，以分隔輸出中的資料行。 沒有選項可用於指定*自訂*的資料行分隔符號。  
  
|值|說明|  
|-----------|-----------------|  
|**{CR}{LF}**|資料行是使用歸位/換行字元組合進行分隔。|  
|**{CR}**|資料行是使用歸位字元進行分隔。|  
|**{LF}**|資料行是使用換行字元進行分隔。|  
|**分號 {;}**|資料行是使用分號進行分隔。|  
|**冒號 {:}**|資料行是使用冒號進行分隔。|  
|**逗號 {,}**|資料行是使用逗號進行分隔。|  
|**定位字元 {t}**|資料行是使用定位字元進行分隔。|  
|**分隔號 {&#124;}**|資料行使用分隔號進行分隔。|  

## <a name="optionally-review-column-mappings-and-preview-data"></a>您可以選擇檢查資料行對應及預覽資料

**編輯對應**   
選擇性地按一下 [編輯對應]，顯示所選取資料表的 [資料行對應] 對話方塊。 使用 [資料行對應]  對話方塊即可執行下列動作。
-   檢閱個別資料行在來源與目的地之間的對應。
-   您可以針對不想要複製的資料行選取 [忽略]  ，只複製資料行的子集。

如需詳細資訊，請參閱 [資料行對應](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。  

**預覽**  
在 [預覽資料] 對話方塊中，選擇性地按一下 [預覽] 預覽最多 200 個取樣資料列。 這會確認精靈即將複製您想要複製的資料。 如需詳細資訊，請參閱 [預覽資料](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)。  
  
在您預覽資料之後，可能會想要變更已在精靈的先前頁面上選取的選項。 若要進行這些變更，請返回 [設定一般檔案目的地]  頁面，然後按一下 [上一步]  返回先前的頁面，如此您就可以在其中變更選取項目。  

## <a name="whats-next"></a>下一步  
 指定目的地一般檔案的格式化選項之後，下一個頁面是 [Save and Execute Package (儲存和執行封裝)] 。 在此頁面上，您可以指定是否要立即執行作業。 根據您的設定，也可以將設定儲存為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) 套件進行自訂並在稍後重複使用。 如需詳細資訊，請參閱 [儲存和執行封裝](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。  

