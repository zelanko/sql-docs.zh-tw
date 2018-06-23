---
title: DISCOVER_LITERALS 資料列集 |Microsoft 文件
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
api_name:
- DISCOVER_LITERALS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_LITERALS rowset
ms.assetid: 1bf0a2e2-a419-4c25-b271-37dfa44de2ea
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a4643ab803f3e6a7d63c4172423e909b6badd64b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033965"
---
# <a name="discoverliterals-rowset"></a>DISCOVER_LITERALS 資料列集
  傳回 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 提供者所支援常值的相關資訊，包括資料類型和值。  
  
 如果您呼叫[探索](../../xmla/xml-elements-methods-discover.md)方法`DISCOVER_LITERALS`中的列舉值[RequestType](../../xmla/xml-elements-properties/type-element-xmla.md)項目，`Discover`方法會傳回`DISCOVER_LITERALS`資料列集。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_LITERALS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`LiteralName`|`DBTYPE_WSTR`||資料列中所描述常值的名稱。<br /><br /> 例如： `DBLITERAL_LIKE_PERCENT`|  
|`LiteralValue`|`DBTYPE_WSTR`||實際的常值。<br /><br /> 例如，如果 `LiteralName` 是 `DBLITERAL_LIKE_PERCENT`，而百分比字元 (`%`) 符合 LIKE 子句中零個或更多個字元，則 `LiteralValue` 資料行的值為 "`%`"。|  
|`LiteralInvalidChars`|`DBTYPE_WSTR`||常值中無效的字元。<br /><br /> 例如，如果資料表名稱可以包含數值字元以外的任何字元，則此字串為 "`0123456789`"。|  
|`LiteralInvalidStartingChars`|`DBTYPE_WSTR`||無法做為常值第一個字元的字元。 如果常值可以用任何有效字元開頭，則此值為 `null`。|  
|`LiteralMaxLength`|`DBTYPE_I4`||常值中的最大字元數。 如果沒有最大數或者不知道最大數，則此值為 -1。|  
|`LiteralNameEnumValue`|`DBTYPE_I4`|||  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 下表中的資料行上可以限制 `DISCOVER_LITERALS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`LiteralName`|`DBTYPE_WSTR`|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)   
 [DISCOVER_KEYWORDS 資料列集&#40;XMLA&#41;](discover-keywords-rowset-xmla.md)  
  
  