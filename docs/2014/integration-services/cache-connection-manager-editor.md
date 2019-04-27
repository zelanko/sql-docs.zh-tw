---
title: 快取連接管理員編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.cacheconnection.f1
ms.assetid: 0d8f9324-0c35-4eea-b06d-da3cc2426d2c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: af7696c1d5194af721b6ff803736193db0285b8b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771719"
---
# <a name="cache-connection-manager-editor"></a>快取連接管理員編輯器
  快取連接管理員會從快取轉換或快取檔案 (.caw) 中讀取參考資料集，而且可以將資料儲存至快取檔案。 資料永遠會儲存在記憶體中。  
  
> [!NOTE]  
>  快取連接管理員不支援二進位大型物件 (BLOB) 資料類型 DT_TEXT、DT_NTEXT 和 DT_IMAGE。 如果參考資料集包含 BLOB 資料類型，則在您執行封裝時元件會失敗。 您可以使用 **[快取連接管理員編輯器]** 修改資料行資料類型。  
  
 查閱轉換會針對參考資料集執行查閱。  
  
 [快取連線管理員編輯器] 對話方塊包含下列索引標籤：  
  
-   [一般 索引標籤](#generaltab)  
  
-   [資料行索引標籤](#columnstab)  
  
 若要深入了解快取連接管理員，請參閱＜ [Cache Connection Manager](connection-manager/cache-connection-manager.md)＞。  
  
##  <a name="generaltab"></a> General Tab  
 使用 [快取連線管理員編輯器] 對話方塊的 [一般] 索引標籤即可指出要從檔案中讀取快取，還是要將快取儲存至檔案。  
  
### <a name="options"></a>選項。  
 **連線管理員名稱**  
 提供唯一的名稱給工作流程中的快取連接。 提供的名稱將顯示在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師內。  
  
 **說明**  
 描述連接。 最佳作法是根據其用途描述連接，使封裝可以自我記錄並易於維護。  
  
 **使用檔案快取**  
 指出是否要使用快取檔案。  
  
> [!NOTE]  
>  封裝保護等級不會套用至快取檔案。 如果快取檔案包含機密資訊，請使用存取控制清單 (ACL) 限制對其中儲存檔案的位置或資料夾的存取權。 您應該只啟用特定帳戶的存取權。 如需詳細資訊，請參閱 [對封裝使用之檔案的存取權](../../2014/integration-services/access-to-files-used-by-packages.md)。  
  
 如果您將快取連接管理員設定為使用快取檔案，連接管理員將進行下列其中一項動作：  
  
-   當「快取轉換」轉換設定為將資料流程中資料來源的資料寫入快取連接管理員時，將資料儲存至檔案。 如需詳細資訊，請參閱 [Cache Transform](data-flow/transformations/cache-transform.md)。  
  
-   從快取檔案中讀取資料。  
  
 **檔案名稱**  
 輸入快取檔案的路徑和檔案名稱。  
  
 **瀏覽**  
 找出快取檔案。  
  
 **重新整理中繼資料**  
 在快取連接管理員中，刪除資料行中繼資料，然後將選取快取檔案的資料行中繼資料重新填入快取連接管理員。  
  
##  <a name="columnstab"></a> 資料行索引標籤  
 使用 **[快取連接管理員編輯器]** 對話方塊的 **[資料行]** 索引標籤即可設定快取中每個資料行的屬性。  
  
### <a name="options"></a>選項。  
 **資料行**  
 指定資料行名稱。  
  
 **索引位置**  
 指定每個資料行的索引位置，藉以指定哪些資料行是索引資料行。 此索引是一或多個資料行的集合。  
  
 如果是非索引資料行，索引位置為 0。  
  
 如果是索引資料行，則索引位置是循序的正數。 這個數目表示查閱轉換比較參考資料集中的資料列與輸入資料來源中的資料列所依據的順序。 擁有最多唯一值的資料行應該有最低的索引位置。  
  
> [!NOTE]  
>  當查閱轉換是設定為使用快取連接管理員，則只有參考資料集中的索引資料行可以對應到輸入資料行。 而且，所有的索引資料行都必須進行對應。  
  
 **型別**  
 指定資料行的資料類型。  
  
 `Length`  
 指定資料行資料類型。 如果適用於資料類型，您可以更新 `Length`。  
  
 `Precision`  
 針對特定資料行資料類型指定有效位數。 位數 (Precision) 是指數字中總共的位數。 如果適用於資料類型，您可以更新 `Precision`。  
  
 `Scale`  
 針對特定資料行資料類型指定小數位數。 小數位數 (Scale) 則是指數字中小數點右方的位數。 如果適用於資料類型，您可以更新 `Scale`。  
  
 `Code Page`  
 指定資料行類型的字碼頁。 如果適用於資料類型，您可以更新 `Code Page`。  
  
## <a name="see-also"></a>另請參閱  
 [Lookup Transformation](data-flow/transformations/lookup-transformation.md)  
  
  
