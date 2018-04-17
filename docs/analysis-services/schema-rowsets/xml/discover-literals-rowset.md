---
title: DISCOVER_LITERALS 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DISCOVER_LITERALS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_LITERALS rowset
ms.assetid: 1bf0a2e2-a419-4c25-b271-37dfa44de2ea
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ae4dfbe2c5f7d9ce9281dd483b7544fb358dd1df
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="discoverliterals-rowset"></a>DISCOVER_LITERALS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]傳回常值，包括資料類型和所支援的值的相關資訊[!INCLUDE[msCoName](../../../includes/msconame-md.md)]XML for Analysis (XMLA) 提供者。  
  
 如果您呼叫[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法**DISCOVER_LITERALS**中的列舉值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)項目，**探索**方法會傳回**DISCOVER_LITERALS**資料列集。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_LITERALS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|**LiteralName**|**DBTYPE_WSTR**||資料列中所描述常值的名稱。<br /><br /> 例如： **DBLITERAL_LIKE_PERCENT**|  
|**LiteralValue**|**DBTYPE_WSTR**||實際的常值。<br /><br /> 例如，如果**LiteralName**是**DBLITERAL_LIKE_PERCENT**和百分比字元 (**%**) 比對零個或多個字元，在 LIKE 子句中，值**LiteralValue**資料行是"**%**"。|  
|**LiteralInvalidChars**|**DBTYPE_WSTR**||常值中無效的字元。<br /><br /> 例如，如果資料表名稱可以包含數字的字元以外的任何項目，這個字串是 「**0123456789**"。|  
|**LiteralInvalidStartingChars**|**DBTYPE_WSTR**||無法做為常值第一個字元的字元。 如果常值可以用任何有效字元開始，這是**null**。|  
|**LiteralMaxLength**|**DBTYPE_I4**||常值中的最大字元數。 如果沒有最大數或者不知道最大數，則此值為 -1。|  
|**LiteralNameEnumValue**|**DBTYPE_I4**|||  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_LITERALS**上表中的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**LiteralName**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [DISCOVER_KEYWORDS 資料列集 &#40;XMLA &#41;](../../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)  
  
  
