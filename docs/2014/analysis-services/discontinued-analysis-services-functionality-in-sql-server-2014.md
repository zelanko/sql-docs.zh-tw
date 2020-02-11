---
title: SQL Server 2014 中已停止的 Analysis Services 功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, backward compatibility
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
- discontinued functionality [Analysis Services]
- unsupported features [Analysis Services]
ms.assetid: 39406be1-9819-4629-9c29-b32fb20bab2e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 616c39d03ff8081c209a80dcca912d831bcef1ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081679"
---
# <a name="discontinued-analysis-services-functionality-in-sql-server-2014"></a>SQL Server 2014 中已停止的 Analysis Services 功能
  本主題描述 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中不再可用的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。  
  
## <a name="discontinued-features-in-includesssql14includessssql14-mdmd"></a>
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]
  
  
|類別|已被取代的功能|取代|  
|--------------|------------------------|-----------------|  
|本機 Cube|InsertInto 連接字串屬性|填入本機 Cube 的原始連接字串語法已被 Create Global Cube 陳述式取代。 如需詳細資訊，請參閱[CREATE GLOBAL CUBE 語句 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-global-cube)。|  
|本機 Cube|CreateCube 連接字串屬性|填入本機 Cube 的原始連接字串語法已被 Create Global Cube 陳述式取代。 如需詳細資訊，請參閱[CREATE GLOBAL CUBE 語句 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-global-cube)。|  
|資料採礦|SQL Server 2000 PMML|SQL Server 2000 PMML 功能會產生擁有專屬延伸模組的一種 PMML，以支援由資料採礦演算法所提供，而在 PMML 規格中沒有的獨特功能。 在 SQL Server 2005 中，Analysis Services 已將 PMML 功能更新為較新的 PMML 2.1 標準。 因此不再需要 SQL Server 2000 中加入的專屬延伸模組 (不過，在這個版本中仍支援)。|  
|MDX 陳述式|Create Action 陳述式|包含此陳述式是為了回溯相容性 (Backward Compatibility) 的需要。 此陳述式已被 Action 物件取代。 如需如何在最新版本中建立動作的詳細[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]資訊，請參閱[&#40;Analysis Services 多維度資料&#41;的動作](multidimensional-models/actions-analysis-services-multidimensional-data.md)。|  
  
## <a name="discontinued-features-in-previous-releases"></a>之前的版本已停止的功能  
 已不再使用移轉精靈 (用來將 SQL Server 2000 Analysis Services 資料庫移轉至較新版本)，因為已不再支援 SQL Server 2000。  
  
 此外，也已不再使用決策支援物件 (DSO) 程式庫 (可提供與 SQL Server 2000 Analysis Services 的相容性)，並且此部分從 SQL Server 中剔除。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Backward Compatibility](analysis-services-backward-compatibility.md)  
  
  
