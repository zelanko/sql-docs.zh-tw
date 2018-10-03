---
title: （MDS 增益集適用於 Excel） 載入之前篩選資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: 9e30eae0-776b-4a09-aac3-0c0249d92ca5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 828205b1786d2539e81dd54317ab0dc0a15e8a6c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48111901"
---
# <a name="filter-data-before-loading-mds-add-in-for-excel"></a>在載入之前篩選資料 (適用於 Excel 的 MDS 增益集)
  在  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]，篩選資料，當您想要限制載入 Excel 的資料範圍的大小。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。  
  
### <a name="to-filter-data-before-loading"></a>若要在載入之前篩選資料  
  
1.  開啟 Excel，然後在 **[主要資料]** 索引標籤上，連接到 MDS 儲存機制。 如需詳細資訊，請參閱[連接到 MDS 儲存機制 &#40;適用於 Excel 的 MDS 增益集&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md)。  
  
2.  在 [主資料總管] 窗格中，選取模型和版本。 系統就會填入實體的清單。  
  
    -   如果沒有顯示 **[主資料總管]** 窗格，請按一下 **[連接和載入]** 群組中的 **[顯示總管]**。  
  
    -   如果 **[主資料總管]** 窗格已停用，這是因為現有的工作表已經包含 MDS 管理的資料。 若要啟用此窗格，請開啟新的工作表。  
  
3.  在 **[主資料總管]** 窗格的實體清單中，按一下您想要篩選的實體。  
  
4.  在功能區上，按一下 **[連接和載入]** 群組中的 **[篩選]**。  
  
5.  選取要顯示的屬性 (資料行)、設定資料行的順序，並且視需要篩選資料以傳回較少資料列，藉以完成 **[篩選]** 對話方塊。 您可以檢視 **[摘要]** 窗格，以便了解系統即將傳回的資料量。 如需詳細資訊，請參閱[篩選對話方塊 &#40;適用於 Excel 的 MDS 增益集&#41;](filter-dialog-box-mds-add-in-for-excel.md)。  
  
6.  按一下 **[載入資料]**。 工作表就會填入 MDS 管理的資料。  
  
    > [!NOTE]  
    >  -   只有前 1 百萬個成員會載入 Excel 中。  
    > -   在條件約束之清單 （網域屬性） 的資料行，會載入前 1000 個的值。  
  
## <a name="next-steps"></a>後續步驟  
 [從 Excel 發行資料給 MDS &#40;MDS 增益集的 Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>另請參閱  
 [載入資料&#40;MDS 增益集的 Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [篩選對話方塊 &#40;適用於 Excel 的 MDS 增益集&#41;](filter-dialog-box-mds-add-in-for-excel.md)   
 [重新排列資料行&#40;MDS 增益集的 Excel&#41;](reorder-columns-mds-add-in-for-excel.md)  
  
  
