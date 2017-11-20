---
title: "將資料從 Excel 匯入 Master Data Services (適用於 Excel 的 MDS 增益集) | Microsoft Docs"
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
ms.assetid: 89fce454-a816-4b33-a26a-d1b9741d269b
caps.latest.revision: 10
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 3051e6d5cbeef00ce4b05ee03bc39e79271207be
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="import-data-from-excel-to-master-data-services-mds-add-in-for-excel"></a>將資料從 Excel 匯入 Master Data Services (適用於 Excel 的 MDS 增益集)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，若您已結束使用 Excel 且想要儲存變更，以讓其他使用者能夠存取，請將資料發行至 MDS 儲存機制。  
  
> [!NOTE]  
>  -   當您發行變更時，系統會刪除 MDS 管理之資料格的註解。  
> -   MDS 管理的資料格中不支援公式。 MDS 管理之資料格中的公式會處理為文字值。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。  
  
-   使用中工作表必須包含 MDS 管理的資料，而且您必須已經對 MDS 管理的資料進行變更或加入作業。  
  
-   如果您要加入成員，而且系統會自動產生實體的代碼，您就不需要指定 **Code** 值。 如需詳細資訊，請參閱[自動建立代碼 &#40;Master Data Services&#41;](../../master-data-services/automatic-code-creation-master-data-services.md)。  
  
### <a name="to-publish-data-to-the-mds-repository"></a>若要將資料發行至 MDS 儲存機制  
  
1.  按一下 [發行和驗證] 群組中的 [發行]。  
  
2.  選擇性。 如果顯示 [發行並註解] 對話方塊，請選擇要針對所有更新共用相同的註解，還是個別註解每個變更。  
  
3.  選擇性。 選取 [不要再顯示這個對話方塊] 核取方塊。 未來，您隨時都可以透過選擇 [設定] 並選取 [發行時顯示發行和註解對話方塊] 核取方塊，顯示此對話方塊。  
  
4.  按一下 [發行]。  
  
> [!NOTE]  
>  如果您要將新的成員 (資料列) 加入至工作表，但是無法順利將它們發行至 MDS 儲存機制，表示您可能沒有工作表中所有屬性的 [更新] 權限。 在 [檢閱] 索引標籤上，按一下 [變更] 群組中的 [取消保護工作表]，再次嘗試發行。  
  
## <a name="next-steps"></a>後續步驟  
 [套用商務規則 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/apply-business-rules-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>另請參閱  
 [概觀：從 Excel 匯入資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)   
 [驗證資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md)  
  
  

