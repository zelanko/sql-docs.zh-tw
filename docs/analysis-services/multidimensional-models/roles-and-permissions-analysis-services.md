---
title: "角色和權限 (Analysis Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [Analysis Services], about security
- security [Analysis Services - multidimensional data], about security
ms.assetid: bb885447-868b-4686-853c-8241f63d4370
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2981ab6e8c529fa24fc2256c93dc903dc58857d7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="roles-and-permissions-analysis-services"></a>角色與權限 (Analysis Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供以角色為基礎的授權模型，授與作業、物件和資料的存取權。 所有存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體或資料庫的使用者都必須在角色的內容中進行存取。  
  
 身為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 系統管理員，您需負責將可無限制存取伺服器上之作業的成員資格授與 **伺服器管理員角色** 。 此角色有固定的權限，無法進行自訂。 依預設，本機 Administrators 群組的成員會自動成為 Analysis Services 系統管理員。  
  
 查詢或處理資料的非管理員使用者是透過 **資料庫角色**來授與存取權。 系統管理員和資料庫管理員都能建立描述指定資料庫內不同存取層級的角色，然後將成員資格指派給每個需要存取的使用者。 每一個角色都有一組自訂權限，可用以存取特定資料庫內的物件和作業。 您可以指派下列層級的權限：資料庫、內部物件如 Cube 和維度 (但不是檢視方塊)，以及資料列。  
  
 常見作法是建立角色並將成員資格指派為個別作業。 通常模型設計人員會在設計階段加入角色。 如此一來，所有角色定義都會反映在定義模型的專案檔案中。 角色成員資格通常是由資料庫管理員建立可開發、測試及執行為獨立作業的指令碼，稍後在資料庫進入實際執行階段時展開。  
  
 所有授權都是基於有效的 Windows 使用者識別。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 只使用 Windows 驗證來驗證使用者識別。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 未提供任何專屬驗證方法。請參閱 [Analysis Services 支援的驗證方法](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)。  
  
> [!IMPORTANT]  
>  每個 Windows 使用者或群組的權限可透過資料庫中的所有角色來加總。 如果一個角色拒絕使用者或群組執行特定工作或檢視特定資料的權限，但另一個角色授與此權限給該使用者或群組，則該使用者或群組將擁有執行此工作或檢視此資料的權限。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [物件和作業的存取權授權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
-   [授與資料庫權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)  
  
-   [授與 Cube 或模型權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)  
  
-   [授與處理權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
-   [授與物件中繼資料的讀取定義權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md)  
  
-   [授與資料來源物件的權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
-   [授與資料採礦結構和模型的權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)  
  
-   [授與維度的權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md)  
  
-   [授與維度資料的自訂存取權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)  
  
-   [授與資料格資料的自訂存取權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
## <a name="see-also"></a>請參閱＜  
 [建立及管理角色 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)  
  
  

