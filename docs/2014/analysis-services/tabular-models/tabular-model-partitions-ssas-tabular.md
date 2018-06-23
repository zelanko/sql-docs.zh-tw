---
title: 表格式模型資料分割 (SSAS 表格式) |Microsoft 文件
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
- sql12.asvs.ssms.partitions.partitionmgr.imbi.f1
ms.assetid: 041c269f-a229-4a41-8794-6ba4b014ef83
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0ce6daee8221b1c87438fc95fd44c3a3a4d7cac5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034854"
---
# <a name="tabular-model-partitions-ssas-tabular"></a>表格式模型資料分割 (SSAS 表格式)
  分割區會將一個資料表分割成多個邏輯部分。 接著，每個分割區可以不受其他分割區的影響，單獨處理 (重新整理)。 模型撰寫期間，在已部署的模型中有重複定義的模型資料分割。 在部署之後，即可使用 **的** [資料分割] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 對話方塊或指令碼，管理這些資料分割及建立新的資料分割。 本主題提供的資訊說明部署的表格式模型資料庫中的資料分割。 如需在模型撰寫期間建立和管理資料分割的詳細資訊，請參閱 [Partitions &#40;SSAS Tabular&#41;](partitions-ssas-tabular.md) (資料分割 (SSAS 表格式))。  
  
 本主題的章節：  
  
-   [優點](#bkmk_benefits)  
  
-   [Permissions](#bkmk_permissions)  
  
-   [處理資料分割](#bkmk_process_partitions)  
  
-   [相關工作](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> 優點  
 有效的模型設計能善加利用分割區，以避免不必要的處理及 Analysis Services 伺服器上之後續處理器的負載，同時，還可確保資料的處理和重新整理頻率能反映資料來源的最新資料。  
  
 例如，表格式模型可能會有「銷售」資料表，其中包括目前 2011 會計年度的銷售資料與之前會計年度的每份銷售資料。 模型的「銷售」資料表具有下列三個資料分割：  
  
|資料分割|來源資料|  
|---------------|---------------|  
|Sales2011|目前會計年度|  
|Sales2010-2001|會計年度 2001 年、2002 年、2003 年、2004 年、2005 年、2006 年。 2007, 2008, 2009, 2010|  
|SalesOld|在過去十年之前的所有會計年度。|  
  
 只要有新的銷售資料新增至目前 2011 會計年度，則必須每天處理該資料，才能精確反映目前會計年度銷售資料分析，因此，Sales2011 資料分割會每晚處理。  
  
 而 Sales2010-2001 資料分割不需要每晚處理；不過，因為之前十個會計年度的銷售資料仍可能會因為產品退貨或其他調整而偶爾變更，所以也必須按時處理，因此 Sales2010-2001 資料分割中的資料會每月處理。 在 SalesOld 資料分割中的資料永遠不會變更，因此只會每年處理一次。  
  
 等到進入 2012 會計年度時，新的 Sales2012 資料分割即會加入模式的「銷售」資料表。 之後，您即可將 Sales2011 資料分割和 Sales2010-2001 資料分割合併，並重新命名為 Sales2011-2002。 2001 會計年度的資料即會從新的 Sales2011-2002 資料分割中刪除，並移至 SalesOld 資料分割中。 如此一來，所有資料分割都已經過處理以反映變更。  
  
 您為組織表格式模型所實作的資料分割策略，主要取決於您的特定模型資料處理需求及可用的資源。  
  
##  <a name="bkmk_permissions"></a> 權限  
 若要在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中建立、管理及處理資料分割，您必須具備在安全性角色中定義的適當 Analysis Services 權限。 每個安全性角色都具有下列其中一個權限：  
  
|權限|動作|  
|----------------|-------------|  
|系統管理員|讀取、處理、建立、複製、合併、刪除|  
|處理|讀取、處理|  
|唯讀|讀取|  
  
 若要深入了解使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 在模型撰寫期間建立角色，請參閱 [Roles &#40;SSAS Tabular&#41;](roles-ssas-tabular.md) (角色 (SSAS 表格式))。 若要深入了解使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 管理已部署表格式模型角色的角色成員，請參閱 [Tabular Model Roles &#40;SSAS Tabular&#41;](tabular-model-roles-ssas-tabular.md) (表格式模型角色 (SSAS 表格式))。  
  
##  <a name="bkmk_process_partitions"></a> 處理資料分割  
 您可使用 **的** [資料分割] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 對話方塊或指令碼，讓資料分割可以不受其他資料分割的影響，單獨處理 (重新整理)。 處理的選項如下：  
  
|[模式]|描述|  
|----------|-----------------|  
|處理預設|偵測資料分割物件的處理狀態，並且執行必要的處理，以便將尚未處理或部分處理的資料分割物件傳遞為完整處理的狀態。 載入空白資料表和資料分割的資料；建立或重新建立階層、導出資料行及關聯性。|  
|完整處理|處理資料分割物件及其包含的所有物件。 對已處理過的物件執行完整處理時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會先卸除該物件中的所有資料，然後再處理該物件。 當物件已進行過任何結構性變更時，就需要這種處理。|  
|處理資料|將資料載入資料分割或資料表，而不重新建立階層或關聯性，或重新計算導出資料行和量值。|  
|處理清除|移除資料分割中的所有資料。|  
|處理加入|以新資料累加地更新資料分割。|  
  
##  <a name="bkmk_related_tasks"></a> 相關工作  
  
|工作|描述|  
|----------|-----------------|  
|[建立及管理表格式模型資料分割&#40;SSAS 表格式&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md)|描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，在部署的表格式模型中建立及管理資料分割。|  
|[處理表格式模型資料分割&#40;SSAS 表格式&#41;](process-tabular-model-partitions-ssas-tabular.md)|描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，在部署的表格式模型中處理資料分割。|  
  
  