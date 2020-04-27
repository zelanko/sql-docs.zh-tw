---
title: 正在完成嚮導（分割區 Wizard） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.finish.f1
ms.assetid: 68a4dd5d-94d9-4a02-be31-949a6da0ef51
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7ab4ad7a819c18056ab5901f95caf1b74b23a25
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087531"
---
# <a name="completing-the-wizard-partition-wizard"></a>正在完成精靈 (資料分割精靈)
  使用 [正在完成精靈]**** 頁面，即可命名資料分割、定義資料分割的彙總設計，以及在完成資料分割精靈之後選擇性地部署和處理資料分割。  
  
## <a name="options"></a>選項。  
 **名稱**  
 輸入新資料分割的名稱。 如果您使用多個資料表，請輸入要和資料表名稱結合的前置詞，以建立每個資料分割名稱。  
  
 **彙總選項**  
 指定資料分割的彙總選項。  
  
 下表列出可用的彙總選項。  
  
|選項|描述|  
|------------|-----------------|  
|**立即設計資料分割的彙總**|在資料分割精靈建立新的資料分割之後，請設計新資料分割的彙總。 在資料分割精靈中按一下 [完成]**** 之後，請選取此選項來啟動彙總設計精靈。 如需 [彙總設計精靈] 的詳細資訊，請參閱 [彙總設計精靈 F1 說明](aggregation-design-wizard-f1-help.md)。|  
|**稍後再設計彙總**|建立資料分割，且不在此時設計彙總。|  
|**從現有的資料分割複製彙總設計**|從量值群組的現有資料分割中，將彙總設計複製到新的資料分割。 按一下此選項，讓 [複製來源]**** 選項可以使用。 使用 [複製來源]**** 選項，即可選取要複製彙總設計的資料分割。<br /><br /> 請注意，未來可能會合並的資料分割必須具有相同的資料表結構和匯總設計。 如果您可能在量值群組中將新的資料分割與現有的資料分割進行合併，則應將現有之資料分割的彙總設計複製到新的資料分割中。|  
  
 **立即部署及處理**  
 針對 [處理與儲存位置]**** 頁面上指定的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體，部署及處理資料分割。 在此頁面上按一下 [完成]**** 之後，精靈就會部署及處理資料分割。  
  
## <a name="see-also"></a>另請參閱  
 [資料分割 &#40;Analysis Services - 多維度資料&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
