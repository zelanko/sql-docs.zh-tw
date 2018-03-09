---
title: "重新排序資料行 (適用於 Excel 的 MDS 增益集) | Microsoft Docs"
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
ms.assetid: ac00462e-c0f7-4b8d-86f2-d9eda2598a15
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 782958cb18c22f39968d33509d4a8366029898b1
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/05/2018
---
# <a name="reorder-columns-mds-add-in-for-excel"></a>重新排序資料行 (適用於 Excel 的 MDS 增益集)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，您可以在載入之前篩選清單，藉以重新排序資料行。  
  
 當您重新排序 **[篩選]** 對話方塊中的屬性時，會使用新的順序，將資料載入至 Excel。 不過，下次您篩選屬性資料時，此順序將會回復到原始設計的順序。 若要永久變更順序，管理員應該在主資料管理員的 **[系統管理]** 區域中變更順序。 如需相關資訊，請參閱 [Change the Order of Attributes](../../master-data-services/change-the-order-of-attributes.md)。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。  
  
### <a name="to-reorder-mds-managed-columns"></a>若要重新排序 MDS 管理的資料行  
  
1.  開啟 Excel，然後在 **[主要資料]** 索引標籤上，連接到 MDS 儲存機制。 如需詳細資訊，請參閱[連接到 MDS 儲存機制 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)。  
  
2.  在 [主資料總管] 窗格中，選取模型和版本。 系統就會填入實體的清單。  
  
    -   如果沒有顯示 **[主資料總管]** 窗格，請按一下 **[連接和載入]** 群組中的 **[顯示總管]**。  
  
    -   如果 **[主資料總管]** 窗格已停用，這是因為現有的工作表已經包含 MDS 管理的資料。 若要啟用此窗格，請開啟新的工作表。  
  
3.  在 **[主資料總管]** 窗格中，按一下實體。  
  
4.  按一下 **[連接和載入]** 群組中的 **[篩選]**。  
  
5.  在 **[篩選]** 對話方塊中，於 **[資料行]** 區段的屬性清單中，按一下您想要移動的屬性。  
  
6.  按一下清單右邊的 **[向上]** 或 **[向下]** 箭號，即可在工作表中向左或向右移動屬性。  
  
7.  針對每個屬性重複步驟 7，直到由上至下順序代表您想要在工作表中呈現的由左至右順序為止。  
  
8.  按一下 **[載入資料]**。 工作表就會填入 MDS 管理的資料，而且資料行會依照您所指定的順序顯示。  
  
## <a name="see-also"></a>另請參閱  
 [概觀：將資料匯出至 Excel &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  
