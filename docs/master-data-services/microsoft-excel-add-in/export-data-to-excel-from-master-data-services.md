---
title: 將資料從 Master Data Services 匯入至 Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: microsoft-excel-add-in
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dd29389b-928c-4e50-995c-c6af27f97805
caps.latest.revision: 16
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 679622c11383fd2e3611b5eaafaf2851db45446c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="export-data-to-excel-from-master-data-services"></a>將資料從 Master Data Services 匯出至 Excel

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，您必須從 MDS 儲存機制匯出資料，才能使用資料。  
  
 如果您想要在載入之前篩選資料集，請改為參閱[在匯出之前篩選資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。  
  
### <a name="to-export-data-from-mds-into-excel"></a>將資料從 MDS 匯出至 Excel  
  
1.  開啟 Excel，然後在 [主要資料] 索引標籤上，連接到 MDS 儲存機制。 如需詳細資訊，請參閱[連接到 MDS 儲存機制 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)。  
  
2.  在 [主資料總管] 窗格中，選取模型和版本。 系統就會填入實體的清單。  
  
    -   如果沒有顯示 **[主資料總管]** 窗格，請按一下 **[連接和載入]** 群組中的 **[顯示總管]**。  
  
    -   如果 **[主資料總管]** 窗格已停用，這是因為現有的工作表已經包含 MDS 管理的資料。 若要啟用此窗格，請開啟新的工作表。  
  
3.  在 [主資料總管] 窗格的實體清單中，按兩下您想要載入的實體。  
  
    > [!NOTE]  
    >  -   只有前 1 百萬個成員會載入 Excel 中。 若要在載入之前篩選清單，在功能區上，按一下 [連接和載入] 群組中的 [篩選]。  
    > -   在屬於受條件約束之清單 (網域屬性) 的資料行中，預設只會載入前 25,000 個值。 您可以在安裝 Excel 所在電腦上的 excelusersettings.config 檔案內，變更 MaximumDbaEntitySize 屬性中的這個數字。 此檔案位於 C:\Users\\<user\>\AppData\Local\Microsoft\Microsoft SQL Server\130\MasterDataServices\\。  
    >   
    >      如果網域屬性的值超過 MaximumDbEntitySize 屬性設定的數目，就不會載入值的清單。  
  
    > [!NOTE]  
    >  如果您使用適用於 Microsoft Excel (32 位元 Excel) 的增益集載入以文字分隔的資料，而且 [Cell Count to Load (要載入的資料格計數)] 和 [Cell Count to Publish (要發行的資料格計數)] 屬性的值都設為最大值 1000，將會發生記憶體不足的錯誤。 您必須使用 64 位元 Excel，才能使用 [Cell Count to Load (要載入的資料格計數)] 和 [Cell Count to Publish (要發行的資料格計數)] 的最大值設定。  
  
## <a name="next-steps"></a>Next Steps  
 [將資料從 Excel 匯入至 Master Data Services &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>另請參閱  
 [概觀：將資料匯出至 Excel &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [篩選對話方塊 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)   
 [概觀：從 Excel 匯入資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
