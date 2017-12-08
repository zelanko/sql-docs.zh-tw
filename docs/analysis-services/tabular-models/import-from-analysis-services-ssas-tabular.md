---
title: "從 Analysis Services (SSAS 表格式) 匯入 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b9a21b23-3a06-4ef8-bc06-9c79cdc54870
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 7c69264c070a5cbae9ed5eee3b6103505633ab4f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="import-from-analysis-services-ssas-tabular"></a>從 Analysis Services 匯入 (SSAS 表格式)
  本主題描述如何使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 [從伺服器匯入] 專案範本，從現有的表格式模型匯入中繼資料，以建立新的表格式模型專案。  
  
## <a name="create-a-new-model-by-importing-metadata-from-an-existing-model-in-analysis-services"></a>從 Analysis Services 中的現有模型匯入中繼資料來建立新的模型  
 您可以使用 [從伺服器匯入] 專案範本從 Analysis Services 伺服器上的現有表格式模型複製中繼資料，以建立新的表格式模型專案。 將會使用與匯入來源之模型相同的資料來源連接、資料表、關聯性、量值、KPI、角色、階層、檢視方塊及資料分割來建立新專案。 但是，資料並不會從現有的模型複製到新模型工作空間。 一旦完成匯入程序並建立新模型專案之後，您必須執行「處理全部」將資料從資料來源載入新模型專案的工作空間資料庫。  
  
#### <a name="to-create-a-new-model-by-importing-metadata-from-an-existing-model"></a>若要從現有的模型匯入中繼資料來建立新模型  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的 **[檔案]** 功能表上，按一下 **[新增]**，然後再按一下 **[專案]**。  
  
2.  在 **[新增專案]** 對話方塊的 **[已安裝的範本]**下，按一下 **[商業智慧]**，然後再按一下 **[從伺服器匯入]**。  
  
3.  在 **[名稱]**中，輸入專案的名稱，並指定位置和方案名稱，然後按一下 **[確定]**。  
  
4.  在 **[從 Analysis Services 匯入]** 對話方塊的 **[伺服器名稱]**中，指定包含您要匯入之模型中繼資料的 Analysis Services 伺服器名稱。  
  
5.  在 **[資料庫名稱]**中，選取包含您要匯入之模型中繼資料的表格式模型資料庫，然後按一下 **[確定]**。  
  
## <a name="see-also"></a>請參閱＜  
 [專案屬性 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  
