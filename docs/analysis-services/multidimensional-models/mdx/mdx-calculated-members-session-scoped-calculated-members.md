---
title: 建立工作階段範圍導出成員 (MDX) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 476c62ef2aa4f0aad3d65cd2b78f27fc9ae6fd7c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021285"
---
# <a name="mdx-calculated-members---session-scoped-calculated-members"></a>MDX 導出成員的工作階段範圍導出成員
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  若要建立可在整個多維度運算式 (MDX) 工作階段取得的導出成員，您可以使用 [CREATE MEMBER](../../../mdx/mdx-data-definition-create-member.md) 陳述式。 使用 CREATE MEMBER 陳述式建立的導出成員，直到 MDX 工作階段結束後才會移除。  
  
 如同本主題所討論，CREATE MEMBER 陳述式的語法直接且使用簡單。  
  
> [!NOTE]  
>  如需建立導出成員的詳細資訊，請參閱[在 MDX 中建立導出成員 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md)。  
  
## <a name="create-member-syntax"></a>CREATE MEMBER 語法  
 使用以下語法將 CREATE MEMBER 陳述式加入 MDX 陳述式：  
  
```  
CREATE [SESSION] MEMBER [<cube-name>.]<fully-qualified-member-name> AS <expression> [,<property-definition-list>]  
<cube name> ::= CURRENTCUBE | <Cube Name>  
<property-definition-list> ::= <property-definition>  
  | <property-definition>, <property-definition-list>  
<property-definition> ::= <property-identifier> = <property-value>  
<property-identifier> ::= VISIBLE | SOLVEORDER | SOLVE_ORDER | FORMAT_STRING | NON_EMPTY_BEHAVIOR <ole db member properties>  
```  
  
 在 CREATE MEMBER 陳述式的語法中， `fully-qualified-member-name` 值是導出成員的完整名稱。 完整名稱包括與導出成員相關的維度或層級。 `expression` 值會在評估過運算式後，傳回導出成員的值。  
  
## <a name="create-member-example"></a>CREATE MEMBER 範例  
 以下範例使用 CREATE MEMBER 陳述式來建立 `LastFourStores` 導出成員。 此導出成員會傳回最後四間商店銷售的單位量總和，而且將可在 Cube 的整個工作階段中使用。  
  
```  
Create Session Member [Store].[Measures].LastFourStores as   
sum(([Stores].[ByLocation].Lag(3) :  
[Stores].[ByLocation].NextMember), [Measures].[Units Sold])  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立查詢範圍導出成員 & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md)  
  
  
