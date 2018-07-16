---
title: XML 資料類型 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- XML data types [XMLA]
- data types [XML for Analysis]
- XMLA, data types
- XML for Analysis, data types
ms.assetid: 979b5384-90d9-4e09-9286-1d1eafdc4864
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9ccba3c69101362d1a384320808a30066ae572b3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37297088"
---
# <a name="xml-data-types-xmla"></a>XML 資料類型 (XMLA)
  除了 XML 1.0 建議所定義的標準基本和衍生類型以外，XML for Analysis (XMLA) 1.1 規格還定義了其他資料類型，可支援多維度和表格式資料的表示。  
  
 XMLA 會使用下表所列的資料類型。  
  
|資料類型|描述|  
|----------------|-----------------|  
|布林|標準的 XML `boolean` 資料類型。|  
|Decimal|標準的 XML `decimal` 資料類型。|  
|[EmptyResult](emptyresult-data-type-xmla.md)|`root` 元素的命名空間。 XMLA 命令不會傳回結果，因為 XMLA 命令通常也不會傳回結果，或是因為發生錯誤時，會傳回此命名空間[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行 XMLA 命令時的執行個體。|  
|[EnumString](enumstring-data-type-xmla.md)|給定列舉值的具名字串常數集合。|  
|Integer|標準的 XML `int` 資料類型。|  
|[MDDataSet](mddataset-data-type-xmla.md)|所傳回的多維度資料*結果*的參數[Execute](../xml-elements-methods-execute.md)方法。|  
|[結果集](resultset-data-type-xmla.md)|`Execute` 方法所傳回的自我描述 XML 結果集。|  
|[Rowset](rowset-data-type-xmla.md)|所傳回的資料來源，內嵌 XML 結構描述，結構化的資料列[探索](../xml-elements-methods-discover.md)方法。|  
|String|XML `string` 資料類型。|  
|UnsignedInt|XML `unsignedInt` 結構描述類型。|  
  
 如需標準 XML 資料類型的完整描述，請參閱全球資訊網協會 (WC3) 的候選建議。  
  
## <a name="see-also"></a>另請參閱  
 [XML 項目&#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)   
 [XML for Analysis &#40;XMLA&#41;參考](../xml-for-analysis-xmla-reference.md)  
  
  
