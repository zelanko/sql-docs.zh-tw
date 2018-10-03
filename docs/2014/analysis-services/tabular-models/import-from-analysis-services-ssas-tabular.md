---
title: 匯入從 Analysis Services (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: b9a21b23-3a06-4ef8-bc06-9c79cdc54870
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8a698ddb598c4de51d4c30dde717176027f67e6d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130499"
---
# <a name="import-from-analysis-services-ssas-tabular"></a>從 Analysis Services 匯入 (SSAS 表格式)
  本主題描述如何使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 [從伺服器匯入] 專案範本，從現有的表格式模型匯入中繼資料，以建立新的表格式模型專案。  
  
## <a name="create-a-new-model-by-importing-metadata-from-an-existing-model-in-analysis-services"></a>從 Analysis Services 中的現有模型匯入中繼資料來建立新的模型  
 您可以使用 [從伺服器匯入] 專案範本從 Analysis Services 伺服器上的現有表格式模型複製中繼資料，以建立新的表格式模型專案。 將會使用與匯入來源之模型相同的資料來源連接、資料表、關聯性、量值、KPI、角色、階層、檢視方塊及資料分割來建立新專案。 但是，資料並不會從現有的模型複製到新模型工作空間。 一旦完成匯入程序並建立新模型專案之後，您必須執行「處理全部」將資料從資料來源載入新模型專案的工作空間資料庫。  
  
#### <a name="to-create-a-new-model-by-importing-metadata-from-an-existing-model"></a>若要從現有的模型匯入中繼資料來建立新模型  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的 **[檔案]** 功能表上，按一下 **[新增]**，然後再按一下 **[專案]**。  
  
2.  在 **[新增專案]** 對話方塊的 **[已安裝的範本]** 下，按一下 **[商業智慧]**，然後再按一下 **[從伺服器匯入]**。  
  
3.  在 **[名稱]** 中，輸入專案的名稱，並指定位置和方案名稱，然後按一下 **[確定]**。  
  
4.  在 **[從 Analysis Services 匯入]** 對話方塊的 **[伺服器名稱]** 中，指定包含您要匯入之模型中繼資料的 Analysis Services 伺服器名稱。  
  
5.  在 **[資料庫名稱]** 中，選取包含您要匯入之模型中繼資料的表格式模型資料庫，然後按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [專案屬性&#40;SSAS 表格式&#41;](properties-ssas-tabular.md)  
  
  
