---
title: 在匯出之前篩選資料 (適用於 Excel 的 MDS 增益集) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9e30eae0-776b-4a09-aac3-0c0249d92ca5
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 003cf7c4871b89067316d2331f658f95a179e37b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65488087"
---
# <a name="filter-data-before-exporting-mds-add-in-for-excel"></a>在匯出之前篩選資料 (適用於 Excel 的 MDS 增益集)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 中，當您想要限制匯入至 Excel 的資料大小或範圍時，請篩選資料。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。  
  
### <a name="to-filter-data-before-exporting"></a>在匯出之前篩選資料  
  
1.  開啟 Excel，然後在 **[主要資料]** 索引標籤上，連接到 MDS 儲存機制。 如需詳細資訊，請參閱[連接到 MDS 儲存機制 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)。  
  
2.  在 [主資料總管]  窗格中，選取模型和版本。 系統就會填入實體的清單。  
  
    -   如果沒有顯示 **[主資料總管]** 窗格，請按一下 **[連接和載入]** 群組中的 **[顯示總管]** 。  
  
    -   如果 **[主資料總管]** 窗格已停用，這是因為現有的工作表已經包含 MDS 管理的資料。 若要啟用此窗格，請開啟新的工作表。  
  
3.  在 **[主資料總管]** 窗格的實體清單中，按一下您想要篩選的實體。  
  
4.  在功能區上，按一下 **[連接和載入]** 群組中的 **[篩選]** 。  
  
5.  選取要顯示的屬性 (資料行)、設定資料行的順序，並且視需要篩選資料以傳回較少資料列，藉以完成 **[篩選]** 對話方塊。 您可以檢視 **[摘要]** 窗格，以便了解系統即將傳回的資料量。 如需詳細資訊，請參閱[篩選對話方塊 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)。  
  
6.  按一下 **[載入資料]** 。 工作表就會填入 MDS 管理的資料。  
  
    > [!NOTE]  
    >  -   只有前 1 百萬個成員會載入 Excel 中。  
    > -   在屬於受條件約束之清單 (網域屬性) 的資料行中，預設只會載入前 25,000 個值。  
  
## <a name="next-steps"></a>後續步驟  
 [將資料從 Excel 匯入至 Master Data Services &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>另請參閱  
 [概觀：將資料匯出至 Excel &#40;MDS 增益集的 Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [篩選對話方塊 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)   
 [重新排序資料行 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/reorder-columns-mds-add-in-for-excel.md)  
  
  
