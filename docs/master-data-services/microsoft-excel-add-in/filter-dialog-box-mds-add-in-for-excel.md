---
title: "篩選對話方塊 (適用於 Excel 的 MDS 增益集) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: microsoft-excel-add-in
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b987b141-5abf-4161-a073-4cfc3e7f5aae
caps.latest.revision: "8"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6e255c0abb98d6ffae0cad9d68fd8696fdef8f71
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="filter-dialog-box-mds-add-in-for-excel"></a>篩選對話方塊 (適用於 Excel 的 MDS 增益集)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 中，若要在將 MDS 管理的資料載入 Excel 之前縮小資料的範圍，請使用 [篩選] 對話方塊。  
  
 這個對話方塊包含三個區段：[資料行]、[資料列] 和 [摘要]。  
  
## <a name="columns"></a>資料行  
 使用 [資料行] 區段可決定您想要在 Excel 中顯示的屬性 (資料行)。  
  
|控制項名稱|說明|  
|------------------|-----------------|  
|屬性類型|屬性類型會描述您想要使用的成員類型。 在大多數情況下，這種類型是 [分葉]。 如需成員類型的詳細資訊，請參閱[成員 &#40;Master Data Services&#41;](../../master-data-services/members-master-data-services.md)。|  
|明確階層|如果您選擇 [合併] 屬性類型，請選擇這些合併成員所屬的階層。 如需詳細資訊，請參閱[明確階層 &#40;Master Data Services&#41;](../../master-data-services/explicit-hierarchies-master-data-services.md)。|  
|屬性群組|屬性群組是將屬性子集分組的方式。 如果您想要顯示可用屬性的子集，請選擇屬性群組。 如需屬性群組的詳細資訊，請參閱[屬性群組 &#40;Master Data Services&#41;](../../master-data-services/attribute-groups-master-data-services.md)。|  
|全選|按一下即可選取清單中顯示的所有屬性。|  
|全部清除|按一下即可清除清單中顯示的選取屬性。<br /><br /> 您無法清除 **Name** 和 **Code**。|  
|向上鍵/向下鍵|按一下即可將選取的屬性在清單中向上或向下移動。 由上至下順序會對應至資料行在工作表中顯示的由左至右順序。|  
  
## <a name="rows"></a>資料列  
 使用 [資料列] 區段可決定您想要在 Excel 中顯示的成員 (資料列)。 您可以透過定義準則進行此作業，以便篩選即將顯示的資料列。  
  
|控制項名稱|說明|  
|------------------|-----------------|  
|Attribute|顯示您想要據以篩選的屬性。 如果沒有列出任何屬性，這是因為尚未加入屬性。<br /><br /> 注意：您可以依照不想要在工作表中顯示的屬性篩選。|  
|運算子|顯示對應至已選取之屬性類型的運算子。 如需詳細資訊，請參閱[篩選運算子 &#40;Master Data Services&#41;](../../master-data-services/filter-operators-master-data-services.md)。|  
|準則|您想要據以篩選的準則。|  
|更新摘要|使用大型資料集時，按一下即可使用即將載入之資料量的詳細資料來更新 [摘要] 區段。|  
|加入|如果您按一下 [資料行] 區段中的屬性，然後按一下 [加入]，屬性就會加入篩選清單中。|  
|全部移除|從清單中移除所有篩選。|  
|移除|從清單中移除選取的篩選。|  
  
## <a name="summary"></a>摘要  
 使用 [摘要] 區段即可在載入之前檢視即將載入之資料量的相關詳細資料。  
  
|控制項名稱|說明|  
|------------------|-----------------|  
|模型|模型的名稱。|  
|版本|版本的名稱。|  
|實體|實體的名稱。|  
|資料列|根據 [資料列] 區段中套用的篩選，即將載入 Excel 中的資料列數目。|  
|資料行|根據 [資料行] 區段中選取的屬性，即將載入 Excel 中的資料行數目。|  
  
## <a name="see-also"></a>另請參閱  
 [在匯出之前篩選資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)   
 [概觀：將資料匯出至 Excel &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  
