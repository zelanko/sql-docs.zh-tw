---
title: "Database 元素 (DTA) 工作負載 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 112fca2a-37e5-4162-b2e7-b56eb8ab0c6f
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e71d9a3077821fc4b34ee5cebac5441065ddf013
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="database-element-for-workload-dta"></a>工作負載的 Database 元素 (DTA)
  指定工作負載追蹤資料表所在的資料庫。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Workload>  
  <Database>  
   ...code removed here...  
  </Database>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|如果未指定任何其他工作負載類型，便需要使用這個元素一次。 您必須指定 **EventString**父系的 **File**、 **Database** 或 **Workload** 子元素，但只能使用一種類型。 例如，如果您利用 **Database** 元素指定了工作負載，便不能在相同 XML 輸入檔中，同時利用 **File** 元素來指定工作負載。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[Workload 元素 &#40; Dta& &#41;](../../tools/dta/workload-element-dta.md)|  
|**子元素**|[資料庫 &#40; Dta& &#41; 的 name 元素](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [資料庫的 Schema 元素 &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>備註  
 在 Database Engine Tuning Advisor XML 結構描述中，這個元素的名稱為 **DatabaseDetailsTypecomplexType** 。 請勿混淆這個 **Database** 元素與根父系是 **Configuration** 元素的元素。 (請參閱[組態的 Database 元素 &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)。)  
  
## <a name="example"></a>範例  
 如需此 **Database** 元素的使用範例，請參閱 [Workload 元素 &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)中的程式碼範例。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

