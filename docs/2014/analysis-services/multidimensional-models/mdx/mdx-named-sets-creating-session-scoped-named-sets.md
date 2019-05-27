---
title: 建立工作階段範圍命名集 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- CREATE SET statement
- session-scoped named sets [MDX]
ms.assetid: b751e1e4-6d4c-4d36-a28d-ffdaaee0f1c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 545bbdb171388f06c28644e0b8caa48db95e7e7f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66074051"
---
# <a name="creating-session-scoped-named-sets-mdx"></a>建立工作階段範圍命名集 (MDX)
  若要建立可在整個多維度運算式 (MDX) 工作階段取得的命名集，您可以使用 [CREATE SET](/sql/mdx/mdx-data-definition-create-set) 陳述式。 使用 CREATE SET 陳述式建立的命名集，直到 MDX 工作階段結束後才會移除。  
  
 如同本主題所討論，WITH 關鍵字的語法直接且使用簡單。  
  
> [!NOTE]  
>  如需命名集的詳細資訊，請參閱[在 MDX 中建立命名集 &#40;MDX&#41;](mdx-named-sets-building-named-sets.md)。  
  
## <a name="create-set-syntax"></a>CREATE SET 語法  
 使用下列 CREATE SET 陳述式的語法：  
  
```  
CREATE SESSION SET [CURRENTCUBE. | <cube name>.]<Set Identifier> AS <Set Expression>  
```  
  
 在 CREATE SET 語法中， `cube name` 參數包含命名集成員的 Cube 名稱。 如果未指定 `cube name` 參數，目前的 Cube 就會做為包含命名集成員的 Cube 使用。 此外， `Set_Identifier` 參數包含命名集的別名，以及包含命名集別名將會參考之集合運算式的 `Set_Expression` 參數。  
  
## <a name="create-set-example"></a>CREATE SET 範例  
 以下範例使用 CREATE SET 陳述式，根據 Store Cube 建立 `SetCities_2_3` 命名集。 `SetCities_2_3` 命名集的成員是在 City 2 及 City 3 內的商店。  
  
```  
create Session set [Store].[SetCities_2_3] as  
{[Data Stores].[ByLocation].[State].&[CA].&[City 02],  
[Data Stores].[ByLocation].[State].&[NH].&[City 03]}  
```  
  
 使用 CREATE SET 陳述式以定義 `SetCities_2_3` 命名集，此命名集就可以在目前的 MDX 工作階段期間內持續使用。 以下範例是一個有效查詢，可傳回 City 2 及 City 3 成員，而且可以在建立 `SetCities_2_3` 命名集之後和工作階段關閉之前隨時執行。  
  
```  
select SetCities_2_3 on 0 from [Store]  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立查詢範圍命名集 &#40;MDX&#41;](mdx-named-sets-creating-query-scoped-named-sets.md)  
  
  
