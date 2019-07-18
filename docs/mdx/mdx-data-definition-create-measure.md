---
title: CREATE MEASURE 陳述式 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e9eb05d633dcbe660c34793fa39c10d788574700
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098377"
---
# <a name="mdx-data-definition---create-measure"></a>MDX 資料定義 - CREATE MEASURE


  在表格式模型中建立量值。  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE MEASURE Table_Name[Measure_Name] = DAX_Expression  
[; CREATE MEASURE ...n]  
  
```  
  
## <a name="arguments"></a>引數  
 *Table_Name*  
 提供將建立量值之資料表名稱的有效字串常值。  
  
 *Measure_Name*  
 提供量值名稱的有效字串常值。  
  
 *DAX_Expression*  
 傳回單一純量值的有效 DAX 運算式。  
  
## <a name="remarks"></a>備註  
 *Measure_Name*必須以方括號括住。  
  
 CREATE MEASURE 陳述式僅適用於在 MDX 指令碼定義中; 內請參閱[MdxScript 元素&#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/objects/mdxscript-element-assl)。  
  
 您也可以定義供單一查詢使用的導出成員。 若要定義受限於單一查詢的導出成員，您可以在 SELECT 陳述式中使用 WITH 子句。 如需詳細資訊，請參閱 <<c0> [ 在 MDX 中建立量值](../analysis-services/multidimensional-models/mdx/mdx-building-measures.md)。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 資料定義陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
