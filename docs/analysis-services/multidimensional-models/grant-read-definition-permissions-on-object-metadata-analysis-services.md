---
title: "授與讀取權限定義物件中繼資料 (Analysis Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- metadata [Analysis Services]
- permissions [Analysis Services], read metadata
- read metadata permissions
ms.assetid: c857e48e-64b0-4ffe-900d-a0a3ddafcefb
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 24e661c0ba9bd5c143365c69282e2cdae91b174a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="grant-read-definition-permissions-on-object-metadata-analysis-services"></a>授與物件中繼資料的讀取定義權限 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]權限讀取的物件定義或中繼資料，在選取的物件上，可讓管理員授與權限來檢視物件詳細資訊，不必同時授與修改物件定義、 修改物件的結構，或檢視的實際權限物件的資料。 [讀取定義] 權限可以在資料庫、資料來源、維度、採礦結構和採礦模型層級上授與。 如果您要求 Cube 的 [讀取定義] 權限，就必須針對資料庫啟用 [讀取定義]。請記住，權限是加總的。 例如，某個角色會授與讀取 Cube 之中繼資料的權限，而第二個角色則會授與讀取維度之中繼資料的相同使用者權限。 兩個不同角色的權限結合之後，使用者就會同時擁有讀取該資料庫內 Cube 之中繼資料和維度之中繼資料的權限。  
  
> [!NOTE]  
>  讀取資料庫之中繼資料的權限，是要使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 連接到 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]資料庫所需的最少權限。 有權限讀取中繼資料的使用者．也可以使用 DISCOVER_XML_METADATA 結構描述資料列集，來查詢物件和檢視其中繼資料。 如需詳細資訊，請參閱 [DISCOVER_XML_METADATA Rowset](../../analysis-services/schema-rowsets/xml/discover-xml-metadata-rowset.md)。  
  
## <a name="set-read-definition-permissions-on-a-database"></a>設定資料庫的讀取定義權限  
 授與讀取資料庫中繼資料的權限時，也會授與讀取資料庫中所有物件之中繼資料的權限。  
  
 建議您在設定用於專用處理的角色時，在資料庫層級包含 [讀取定義] 權限。 擁有 [讀取定義] 可讓非管理員的使用者在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中檢視模型的物件階層，並巡覽到個別物件以執行後續處理。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，在物件總管中展開適當資料庫的 [角色]，然後按一下資料庫角色 (或建立新的資料庫角色)。  
  
2.  在 [一般] 索引標籤上，選取 [讀取定義] 選項。  
  
3.  在 [成員資格] 窗格中，輸入使用這個角色連線到 Analysis Services 的 Windows 使用者和群組帳戶。  
  
4.  按一下 [確定]，完成角色的建立。  
  
## <a name="set-read-definition-permissions-on-individual-objects"></a>設定個別物件的讀取定義權限  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連線到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體、開啟 [資料庫] 資料夾、選取資料庫、在物件總管中展開適當資料庫的 [角色]，然後按一下資料庫角色 (或建立新的資料庫角色)。  
  
2.  在 [一般] 窗格中，清除 [讀取定義] 的資料庫權限。 這個步驟會移除權限繼承，因此，您可以設定個別物件的權限。  
  
3.  選取您正在指定 [讀取定義] 屬性的物件：  
  
    -   在 [資料來源] 窗格中，按一下該資料來源的 [讀取定義] 核取方塊。 角色成員可以檢視連線至資料來源的連線字串，包含伺服器名稱，可能也包含使用者名稱。 如果您想要提供連線字串資訊，可以使用這個權限，不需要同時授與修改連線字串或檢視任何其他物件之定義的權限。  
  
    -   在 [維度] 窗格中，按一下該維度的 [讀取定義] 核取方塊。 有經驗的分析師與開發人員可能需要檢視定義，而不需要修改它或檢視其他物件 (例如，其他維度、Cube 物件，或者採礦結構和模型) 之定義的權限。  
  
    -   在 [採礦結構] 窗格中，按一下資料採礦結構或模型的 [讀取定義] 核取方塊。 需要有 [讀取定義] 才能瀏覽資料模型。 請參閱[授與資料採礦結構和模型的權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)。  
  
4.  在 [成員資格] 窗格中，輸入使用這個角色連線到 Analysis Services 的 Windows 使用者和群組帳戶。  
  
5.  按一下 [確定]，完成角色的建立。  
  
## <a name="see-also"></a>請參閱  
 [授與資料庫權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)   
 [授與處理權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
  
