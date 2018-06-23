---
title: 合併資料分割對話方塊 (Analysis Services-多維度資料) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.sqlserverstudio.mergepartition.f1
ms.assetid: 1c94e250-ee18-4f98-b112-985f6346102a
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: aae229b83f367613cc786a3910b00b45e64f31bd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132984"
---
# <a name="merge-partition-dialog-box-analysis-services---multidimensional-data"></a>合併資料分割對話方塊 (Analysis Services - 多維度資料)
  在 **SQL Server Management Studio** 中，使用 **[合併資料分割]** 對話方塊，即可為 Cube 中的量值群組合併資料分割。 在物件總管中，以滑鼠右鍵按一下 [資料分割] 資料夾或資料分割，然後從操作功能表選取 [合併資料分割]，即可顯示 [合併資料分割] 對話方塊。  
  
## <a name="options"></a>選項。  
 **Server**  
 選取包含目標資料分割之 Analysis Services 執行個體的名稱。  
  
 **名稱**  
 選取現有資料分割的名稱作為目標資料分割。  
  
 **資料夾**  
 如果 [名稱] 中選取的資料分割不使用 Analysis Services 執行個體的預設資料夾，則會顯示包含目標資料分割的資料夾名稱。  
  
 **來源資料分割**  
 顯示方格，其中包含可以合併至目標資料分割的來源資料分割。  
  
> [!NOTE]  
>  只有在相同量值群組中共用相同彙總設計的資料分割可以進行合併。  
  
 方格包含下列資料行：  
  
|「資料行」|描述|  
|------------|-----------------|  
|**合併式**|選取即可將來源資料分割合併至目標資料分割。|  
|**分割區名稱**|顯示來源資料分割的名稱。|  
|**上次處理**|顯示上次處理來源資料分割的日期和時間。|  
  
## <a name="see-also"></a>另請參閱  
 [資料分割&#40;Analysis Services-多維度資料&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Analysis Services 中的資料分割合併&#40;SSAS-多維度&#41;](multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  