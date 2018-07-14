---
title: 主旨區域資料庫結構描述選項 （結構描述產生精靈） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.schemagenwizard.subjectareaschemaopts.f1
ms.assetid: 4c109bb8-e19d-412b-908f-bfdd7f872439
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb617bca3a906162f372ce482269d3fca386acec
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235588"
---
# <a name="subject-area-database-schema-options-schema-generation-wizard-analysis-services---multidimensional-data"></a>主題領域資料庫結構描述選項 (結構描述產生精靈) (Analysis Services - 多維度資料)
  使用 **[主題領域資料庫結構描述選項]** 頁面來控制如何產生結構描述，以及定義如何保留資料。  
  
## <a name="options"></a>選項。  
 **主控結構描述**  
 指定新主題領域資料庫內之結構描述的名稱。  
  
 **在維度資料表上建立主索引鍵**  
 在產生的結構描述中，於維度資料表上建立主索引鍵。 如果您沒有選取此選項，將不會產生任何索引。  
  
> [!NOTE]  
>  如果您沒有選取此選項，將會強制執行參考完整性。  
  
 **建立索引**  
 在產生的結構描述中，於外部索引鍵資料行上建立索引。  
  
 **強制執行參考完整性**  
 在產生的結構描述中，強制執行參考完整性。 如果您沒有選取此選項，將會建立關聯性但不會強制執行。  
  
 **在**  
 當精靈完成時，保留主題領域資料庫中的資料。 如果您沒有選取此選項，將會無預警清除主題領域資料庫中的所有資料。  
  
 **擴展時間資料表**  
 指定精靈如何擴展時間資料表。 下表描述此選項的可能值。  
  
> [!NOTE]  
>  只有在專案模式中使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，從 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 專案中呼叫結構描述產生精靈時，才能啟用此選項。  
  
|值|描述|  
|-----------|-----------------|  
|擴展|已擴展主題領域時間資料表。|  
|不要擴展|不擴展主題領域時間資料表。|  
|只有是空的時才擴展|只有主題領域時間資料表是空的時才擴展。|  
  
## <a name="see-also"></a>另請參閱  
 [結構描述產生精靈 F1 說明&#40;Analysis Services-多維度資料&#41;](schema-generation-wizard-f1-help-analysis-services-multidimensional-data.md)  
  
  
