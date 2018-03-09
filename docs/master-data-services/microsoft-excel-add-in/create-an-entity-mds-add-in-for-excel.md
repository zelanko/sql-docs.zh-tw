---
title: "建立實體 (適用於 Excel 的 MDS 增益集) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: microsoft-excel-add-in
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d354abb3-88fe-4b40-a374-f6256b84ffae
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a344f047e914a798ec34053100f474c7aabcde76
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/05/2018
---
# <a name="create-an-entity-mds-add-in-for-excel"></a>建立實體 (適用於 Excel 的 MDS 增益集)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，系統管理員可以建立新的實體來儲存資料。 當您建立實體時，應該至少載入要儲存的資料樣本。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 [系統管理] 和總管功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
-   您必須有要在其中建立實體的現有模型。 如需詳細資訊，請參閱[建立模型 &#40;Master Data Services&#41;](../../master-data-services/create-a-model-master-data-services.md)。  
  
-   確定您的資料符合下列需求：  
  
    -   資料應該具有標頭資料列。  
  
    -   具有 **Name** 和 **Code** 資料行是有幫助的。 **Code** 是每個資料列的唯一識別碼。  
  
    -   除了標頭以外，應該至少還有一個資料列。 並不是所有資料行都需要值，但資料應該有代表性，可代表實體中的未來資料。  
  
    -   如果您有包含唯一識別碼 (在 MDS 中稱為 **Code**) 的資料行，請確定值是唯一的。 如果沒有資料行包含識別碼，可在建立實體時讓它們自動產生。  
  
    -   確定沒有資料格包含公式。  
  
    -   確定沒有資料格包含時間值。 日期值可儲存在 MDS 中，但時間值不能。  
  
### <a name="to-create-an-entity-and-load-data"></a>若要建立實體及載入資料  
  
1.  開啟或建立 Excel 工作表，其中包含您要載入的資料。  
  
2.  選取要載入到新實體的資料格。  
  
3.  在 [主要資料] 索引標籤的 [建立模型] 群組中，按一下 [建立實體]。  
  
4.  如果系統提示您連接到 MDS 儲存機制，請連接。  
  
5.  在 [建立實體] 對話方塊中，保持預設的範圍，或加以變更以套用至要載入的資料。  
  
6.  請不要清除 [我的資料有標題] 核取方塊。  
  
7.  從 **[模型]** 清單中選取模型。  
  
8.  從 **[版本]** 清單中選取版本。  
  
9. 在 [新實體名稱] 方塊中，輸入實體的名稱。  
  
10. 從 **Code** 清單中，選取包含唯一識別碼的資料行或讓系統自動產生代碼。  
  
11. 選擇性。 從 [名稱] 清單中，選取包含每個成員名稱的資料行。  
  
12. 按一下 [確定] 。 成功建立實體時，畫面上會顯示新標頭資料列，反白顯示資料格，而且更新工作表名稱以符合實體名稱。  
  
## <a name="next-steps"></a>Next Steps  
  
-   若要檢視發生的錯誤，請按一下 [發行和驗證] 群組中的 [顯示狀態]。 ValidationStatus 和 InputStatus 資料行隨即顯示。 如需詳細資訊，請參閱[驗證資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md)。  
  
-   確認屬性已建立為預期的資料類型。  
  
## <a name="see-also"></a>另請參閱  
 [建立網域屬性 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)  
  
  
