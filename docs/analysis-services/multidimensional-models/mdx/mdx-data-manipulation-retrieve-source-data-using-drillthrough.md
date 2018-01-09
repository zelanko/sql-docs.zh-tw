---
title: "使用 DRILLTHROUGH 擷取來源資料 (MDX) |Microsoft 文件"
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
- DRILLTHROUGH statement
- retrieving data
- queries [MDX], DRILLTHROUGH statement
- data retrieval [MDX]
ms.assetid: fe0ab170-25a9-45a8-a377-f71a67f77018
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1749970e49904d8788c08f8be29cd20d189ebca3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-manipulation---retrieve-source-data-using-drillthrough"></a>MDX 資料操作使用 DRILLTHROUGH 擷取來源資料
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]多維度運算式 (MDX) 使用[鑽研](../../../mdx/mdx-data-manipulation-drillthrough.md)cube 資料格的資料來源擷取資料列集的陳述式。  
  
 必須定義 Cube 的鑽研動作，才能在該 Cube 上執行 **DRILLTHROUGH** 陳述式。 若要定義鑽研動作，請在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 的 Cube 設計師中，於 [動作] 窗格的工具列上，按一下 [新增鑽研動作]。 在 [新增鑽研動作] 中，指定動作名稱、目標、條件，以及 **DRILLTHROUGH** 陳述式所傳回的資料行。  
  
## <a name="drillthrough-statement-syntax"></a>DRILLTHROUGH 陳述式語法  
 **DRILLTHROUGH** 陳述式使用以下語法：  
  
```  
<drillthrough> ::= DRILLTHROUGH [<Max_Rows>] [<First_Rowset>] <MDX select> [<Return_Columns>]  
   < Max_Rows> ::= MAXROWS <positive number>  
   <First_Rowset> ::= FIRSTROWSET <positive number>  
   <Return_Columns> ::= RETURN <member or attribute> [, <member or attribute>]  
```  
  
 **SELECT** 子句可識別包含所要擷取之來源資料的 Cube 資料格。 除了在 **SELECT** 子句中每個軸只能指定一個成員之外，此 **SELECT** 子句與一般 MDX **SELECT** 陳述式相同。 如果在一個座標軸上指定多個成員，就會發生錯誤。  
  
 `<Max_Rows>` 語法可指定每個傳回之資料列集中的最大資料列數目。 如果用以連接資料來源的 OLE DB 提供者不支援 **DBPROP_MAXROWS**，就會忽略 `<Max_Rows>` 設定。  
  
 `<First_Rowset>` 語法可識別最早將資料列集傳回的資料分割。  
  
 `<Return_Columns>` 語法可識別要傳回的基礎資料庫資料行。  
  
## <a name="drillthrough-statement-example"></a>DRILLTHROUGH 陳述式範例  
 以下範例示範 **DRILLTHROUGH** 陳述式的用法。 在此範例中，DRILLTHROUGH 陳述式會沿著 Stores 維度 (Slicer 軸)，查詢 Store、Product 及 Time 維度的分葉，然後傳回部門量值群組、部門識別碼及員工的姓氏。  
  
```  
DRILLTHROUGH  
Select {Leaves(Store), Leaves(Product), Leaves(Time),*} on 0  
From Stores  
RETURN [Department MeasureGroup].[Department Id], [Employee].[First Name]  
```  
  
## <a name="see-also"></a>請參閱  
 [操作資料 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  
