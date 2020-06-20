---
title: 篩選對話方塊 (適用於 Excel 的 MDS 增益集) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b987b141-5abf-4161-a073-4cfc3e7f5aae
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ac7c811c6f823b20a99fa590b48448d4b8ca3dbf
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84961098"
---
# <a name="filter-dialog-box-mds-add-in-for-excel"></a>篩選對話方塊 (適用於 Excel 的 MDS 增益集)
  在中 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] ，您可以使用 [**篩選**] 對話方塊，在將 MDS 管理的資料載入 Excel 之前縮小其清單範圍。  
  
 這個對話方塊包含三個區段：[資料行]****、[資料列]**** 和 [摘要]****。  
  
## <a name="columns"></a>資料行  
 使用 [資料行]**** 區段可決定您想要在 Excel 中顯示的屬性 (資料行)。  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|屬性類型|屬性類型會描述您想要使用的成員類型。 在大多數情況下，這種類型是 [分葉]****。 如需成員類型的詳細資訊，請參閱[成員 &#40;Master Data Services&#41;](../members-master-data-services.md)。|  
|明確階層|如果您選擇 [合併]**** 屬性類型，請選擇這些合併成員所屬的階層。 如需詳細資訊，請參閱 [明確階層 &#40;Master Data Services&#41;](../explicit-hierarchies-master-data-services.md)。|  
|屬性群組|屬性群組是將屬性子集分組的方式。 如果您想要顯示可用屬性的子集，請選擇屬性群組。 如需屬性群組的詳細資訊，請參閱[屬性群組 &#40;Master Data Services&#41;](../attribute-groups-master-data-services.md)。|  
|全選|按一下即可選取清單中顯示的所有屬性。|  
|全部清除|按一下即可清除清單中顯示的選取屬性。<br /><br /> 注意：您無法清除**名稱**和程式**代碼**。|  
|向上箭號|按一下即可將選取的屬性在清單中向上移動。 由上至下順序會對應至資料行在工作表中顯示的由左至右順序。|  
|向下箭號|按一下即可將選取的屬性在清單中向下移動。 由上至下順序會對應至資料行在工作表中顯示的由左至右順序。|  
  
## <a name="rows"></a>資料列  
 使用 [資料列]**** 區段可決定您想要在 Excel 中顯示的成員 (資料列)。 您可以透過定義準則進行此作業，以便篩選即將顯示的資料列。  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|屬性|顯示您想要據以篩選的屬性。 如果沒有列出任何屬性，這是因為尚未新增屬性。<br /><br /> 注意：您可以依照不想要在工作表中顯示的屬性來篩選。|  
|運算子|顯示對應至已選取之屬性類型的運算子。 如需詳細資訊，請參閱[篩選運算子 &#40;Master Data Services&#41;](../filter-operators-master-data-services.md)。|  
|準則|您想要據以篩選的準則。|  
|更新摘要|使用大型資料集時，按一下即可使用即將載入之資料量的詳細資料來更新 [摘要]**** 區段。|  
|加|如果您按一下 [資料行]**** 區段中的屬性，然後按一下 [加入]****，屬性就會加入篩選清單中。|  
|全部移除|從清單中移除所有篩選。|  
|移除|從清單中移除選取的篩選。|  
  
## <a name="summary"></a>摘要  
 使用 [摘要]**** 區段即可在載入之前檢視即將載入之資料量的相關詳細資料。  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|模型|模型的名稱。|  
|版本|版本的名稱。|  
|單位|實體的名稱。|  
|資料列|根據 [資料列]**** 區段中套用的篩選，即將載入 Excel 中的資料列數目。|  
|資料行|根據 [資料行]**** 區段中選取的屬性，即將載入 Excel 中的資料行數目。|  
  
## <a name="see-also"></a>另請參閱  
 [載入 &#40;適用于 Excel 的 MDS 增益集之前先篩選資料&#41;](filter-data-before-exporting-mds-add-in-for-excel.md)   
 [載入適用于 Excel 的 MDS 增益集&#41;的資料 &#40;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  
