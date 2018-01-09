---
title: "DISCOVER_KEYWORDS 資料列集 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DISCOVER_KEYWORDS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_KEYWORDS rowset
ms.assetid: 99945e53-3a1b-4d7b-9aff-712977db8b2d
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0529692c18cb33848bf74bd7ed2c2e64dcdebe74
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="discoverkeywords-rowset-xmla"></a>DISCOVER_KEYWORDS 資料列集 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]傳回所保留關鍵字的相關資訊[!INCLUDE[msCoName](../../../includes/msconame-md.md)]XML for Analysis (XMLA) 提供者。  
  
 如果您呼叫[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法**DISCOVER_KEYWORDS**中的列舉值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)項目，**探索**方法會傳回**DISCOVER_KEYWORDS**資料列集。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_KEYWORDS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|**關鍵字**|**DBTYPE_WSTR**||提供者保留的所有關鍵字的清單。<br /><br /> 範例： **AND**|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_KEYWORDS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**關鍵字**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [DISCOVER_LITERALS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-literals-rowset.md)  
  
  
