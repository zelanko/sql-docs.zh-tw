---
title: 合併資料分割對話方塊（Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.mergepartition.f1
ms.assetid: 1c94e250-ee18-4f98-b112-985f6346102a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26751f2cc00330716f160c115d0e839cc6d9527a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66077833"
---
# <a name="merge-partition-dialog-box-analysis-services---multidimensional-data"></a>合併資料分割對話方塊 (Analysis Services - 多維度資料)
  在 **SQL Server Management Studio** 中，使用 **[合併資料分割]** 對話方塊，即可為 Cube 中的量值群組合併資料分割。 在物件總管**** 中，以滑鼠右鍵按一下 [資料分割] 資料夾或資料分割，然後從操作功能表選取 [合併資料分割]****，即可顯示 [合併資料分割]**** 對話方塊。  
  
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
  
|資料行|描述|  
|------------|-----------------|  
|**合併式**|選取即可將來源資料分割合併至目標資料分割。|  
|**資料分割名稱**|顯示來源資料分割的名稱。|  
|**上次處理**|顯示上次處理來源資料分割的日期和時間。|  
  
## <a name="see-also"></a>另請參閱  
 [分割區 &#40;Analysis Services 多維度資料&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [在 Analysis Services 中合併資料分割 &#40;SSAS-多維度&#41;](multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  
