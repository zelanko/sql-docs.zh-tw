---
title: 授與讀取權限定義物件中繼資料 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- metadata [Analysis Services]
- permissions [Analysis Services], read metadata
- read metadata permissions
ms.assetid: c857e48e-64b0-4ffe-900d-a0a3ddafcefb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e03e55451c2340b5f0773e2873127c3551a82aab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074900"
---
# <a name="grant-read-definition-permissions-on-object-metadata-analysis-services"></a>授與物件中繼資料的讀取定義權限 (Analysis Services)
  讀取所選物件上的物件定義或中繼資料的權限，可讓管理員授與檢視物件資訊的權限，而不必同時授與修改物件定義、修改物件結構或檢視物件實際資料的權限。 `Read Definition` 在資料庫、 資料來源、 維度、 採礦結構和採礦模型層級，可以授與權限。 如果您需要`Read Definition`cube 的權限，您必須啟用`Read Definition`資料庫。請記住，權限是加總。 例如，某個角色會授與讀取 Cube 之中繼資料的權限，而第二個角色則會授與讀取維度之中繼資料的相同使用者權限。 兩個不同角色的權限結合之後，使用者就會同時擁有讀取該資料庫內 Cube 之中繼資料和維度之中繼資料的權限。  
  
> [!NOTE]  
>  讀取資料庫之中繼資料的權限，是要使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 連接到 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]資料庫所需的最少權限。 有權限讀取中繼資料的使用者．也可以使用 DISCOVER_XML_METADATA 結構描述資料列集，來查詢物件和檢視其中繼資料。 如需詳細資訊，請參閱 [DISCOVER_XML_METADATA Rowset](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-xml-metadata-rowset)。  
  
## <a name="set-read-definition-permissions-on-a-database"></a>設定資料庫的讀取定義權限  
 授與讀取資料庫中繼資料的權限時，也會授與讀取資料庫中所有物件之中繼資料的權限。  
  
 我們建議您包含`Read Definition`在設定用於專用處理的角色時，資料庫層級的權限。 擁有`Read Definition`可讓非系統管理員可以檢視模型的物件階層中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]並瀏覽至個別的物件進行後續處理。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，在物件總管中展開適當資料庫的 [角色]  ，然後按一下資料庫角色 (或建立新的資料庫角色)。  
  
2.  在 **一般**索引標籤上，選取`Read Definition`選項。  
  
3.  在 [成員資格]  窗格中，輸入使用這個角色連線到 Analysis Services 的 Windows 使用者和群組帳戶。  
  
4.  按一下 [確定]  ，完成角色的建立。  
  
## <a name="set-read-definition-permissions-on-individual-objects"></a>設定個別物件的讀取定義權限  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連線到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體、開啟 [資料庫]  資料夾、選取資料庫、在物件總管中展開適當資料庫的 [角色]  ，然後按一下資料庫角色 (或建立新的資料庫角色)。  
  
2.  在 **一般**窗格中，清除的資料庫權限`Read Definition`。 這個步驟會移除權限繼承，因此，您可以設定個別物件的權限。  
  
3.  選取您要為其指定的物件`Read Definition`屬性：  
  
    -   在 **資料來源**窗格中，按一下 `Read Definition`核取方塊，該資料來源。 角色成員可以檢視連線至資料來源的連線字串，包含伺服器名稱，可能也包含使用者名稱。 如果您想要提供連線字串資訊，可以使用這個權限，不需要同時授與修改連線字串或檢視任何其他物件之定義的權限。  
  
    -   在 **維度**窗格中，按一下 `Read Definition`該維度的核取方塊。 有經驗的分析師與開發人員可能需要檢視定義，而不需要修改它或檢視其他物件 (例如，其他維度、Cube 物件，或者採礦結構和模型) 之定義的權限。  
  
    -   在 採礦結構 窗格中，按一下 `Read Definition`資料採礦結構或模型的核取方塊。 `Read Definition` 需要瀏覽資料模型。 請參閱[授與資料採礦結構和模型的權限 &#40;Analysis Services&#41;](grant-permissions-on-data-mining-structures-and-models-analysis-services.md)。  
  
4.  在 [成員資格]  窗格中，輸入使用這個角色連線到 Analysis Services 的 Windows 使用者和群組帳戶。  
  
5.  按一下 [確定]  ，完成角色的建立。  
  
## <a name="see-also"></a>另請參閱  
 [授與資料庫權限 &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md)   
 [授與處理權限 &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)  
  
  
