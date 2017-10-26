---
title: "設定一般檔案目的地 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: 93fbd5e9429d06e3f011f6f0aff03d76a3db9000
ms.contentlocale: zh-tw
ms.lasthandoff: 10/13/2017

---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>設定一般檔案目的地 (SQL Server 匯入和匯出精靈)
  如果您選取一般檔案目的地，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匯入和匯出精靈 」 會顯示**設定一般檔案目的地**之後您可以指定您想要將資料表複製或提供查詢。 在此頁面上，您可以指定目的地一般檔案的格式化選項。 (選擇性) 您可以檢閱個別資料行的對應，並預覽範例資料。  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>[設定一般檔案目的地] 頁面的螢幕擷取畫面  
 下列螢幕擷取畫面顯示的範例**設定一般檔案目的地**精靈頁面。
 
 在此範例中，使用者已指定下列選項來建立一般 CSV （逗號分隔值） 檔案。
-   **資料列分隔符號**。 每個輸出中的資料列結尾歸位換行字元組合。
-   **資料行分隔符號**。 資料行中每個資料列的資料會以逗號分隔。

 ![設定一般檔案匯入和匯出精靈 頁面](../../integration-services/import-export-data/media/flat-file.png)
  
## <a name="pick-a-source-table"></a>挑選來源資料表
 **來源資料表或檢視表**  
-   如果您指定您想要將資料表複製前一頁上，請從下拉式清單中選取來源資料表或檢視表。
-   如果您提供的查詢，`"Query"`選取，而且為唯一的選項。  

## <a name="specify-row-and-column-delimiters-for-the-output"></a>指定輸出的資料列和資料行分隔符號
 **資料列分隔符號**  
 選取清單中的分隔符號來分隔在輸出中的資料列。 不沒有指定任何選項*自訂*資料列分隔符號。  
  
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
 選取清單中的分隔符號來分隔在輸出中的資料行。 不沒有指定任何選項*自訂*資料行分隔符號。  
  
|值|說明|  
|-----------|-----------------|  
|**{CR}{LF}**|資料行是使用歸位/換行字元組合進行分隔。|  
|**{CR}**|資料行是使用歸位字元進行分隔。|  
|**{LF}**|資料行是使用換行字元進行分隔。|  
|**分號 {;}**|資料行是使用分號進行分隔。|  
|**冒號 {:}**|資料行是使用冒號進行分隔。|  
|**逗號 {,}**|資料行是使用逗號進行分隔。|  
|**定位字元 {t}**|資料行是使用定位字元進行分隔。|  
|**分隔號 {&#124;}**|資料行是使用分隔號進行分隔。|  

## <a name="optionally-review-column-mappings-and-preview-data"></a>（選擇性） 檢閱資料行對應，然後預覽資料

**編輯對應**   
（選擇性） 按一下**編輯對應**顯示**資料行對應**所選取資料表 對話方塊。 使用 [資料行對應]  對話方塊即可執行下列動作。
-   檢閱個別資料行在來源與目的地之間的對應。
-   您可以針對不想要複製的資料行選取 [忽略]  ，只複製資料行的子集。

如需詳細資訊，請參閱 [資料行對應](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。  

**預覽**  
（選擇性） 按一下**預覽**預覽最多 200 個範例中的資料列**預覽資料** 對話方塊。 這會確認精靈即將複製您想要複製的資料。 如需詳細資訊，請參閱 [預覽資料](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)。  
  
在您預覽資料之後，可能會想要變更已在精靈的先前頁面上選取的選項。 若要進行這些變更，請返回 [設定一般檔案目的地]  頁面，然後按一下 [上一步]  返回先前的頁面，如此您就可以在其中變更選取項目。  

## <a name="whats-next"></a>下一步  
 指定目的地一般檔案的格式化選項之後，下一個頁面是 [Save and Execute Package (儲存和執行封裝)] 。 在此頁面上，您可以指定是否要立即執行作業。 根據您設定，您也可以儲存為您設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]加以自訂，以及供日後重複使用的封裝。 如需詳細資訊，請參閱 [儲存和執行封裝](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。  


