---
title: DISCOVER_KEYWORDS 資料列集 (OLE DB for OLAP) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 72c6dd5260ea68f2940a67350b4dae0d5f5e9904
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34028159"
---
# <a name="discoverkeywords-rowset-ole-db-for-olap"></a>DISCOVER_KEYWORDS 資料列集 (OLE DB for OLAP)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  列舉提供者所保留字詞的清單。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 DISCOVER_KEYWORDS 資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**關鍵字**|**DBTYPE_WSTR**||保留的關鍵字。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 DISCOVER_KEYWORDS 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**關鍵字**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
