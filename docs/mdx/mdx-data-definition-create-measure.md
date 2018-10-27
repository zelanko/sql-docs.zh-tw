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
manager: kfile
ms.openlocfilehash: 37a8b8ef757184e7467c3551148c8c149bb45097
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2018
ms.locfileid: "50144454"
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
  
  
