---
title: "CREATE MEASURE 陳述式 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: f264ba96-cbbe-488b-8ac9-b3056a6e997b
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a7becc09d59d729b6f138ceef83e8a7725b3a3b1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="mdx-data-definition---create-measure"></a>MDX 資料定義-建立量值
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
 CREATE MEASURE 陳述式只可用在 MDX 指令碼定義請參閱[MdxScript 元素 &#40;ASSL &#41;](../analysis-services/scripting/objects/mdxscript-element-assl.md).  
  
 您也可以定義供單一查詢使用的導出成員。 若要定義受限於單一查詢的導出成員，您可以在 SELECT 陳述式中使用 WITH 子句。 如需詳細資訊，請參閱[在 MDX 中建立量值](../analysis-services/multidimensional-models/mdx/mdx-building-measures.md)。  
  
## <a name="see-also"></a>請參閱  
 [MDX 資料定義陳述式 &#40;MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
