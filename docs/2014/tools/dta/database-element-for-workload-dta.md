---
title: 工作負載的 Database 元素（DTA） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 112fca2a-37e5-4162-b2e7-b56eb8ab0c6f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9f5b5c233a482672a0cc225364dbf1e4f3b4b645
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63185402"
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
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|如果未指定任何其他工作負載類型，便需要使用這個元素一次。 您必須指定 `EventString` 父系的 `File`、`Database` 或 `Workload` 子元素，但只能使用一種類型。 例如，如果您利用 `Database` 元素指定了工作負載，便不能在相同 XML 輸入檔中，同時利用 `File` 元素來指定工作負載。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[Workload 元素 &#40;DTA&#41;](workload-element-dta.md)|  
|**子元素**|[資料庫的 Name 元素 &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [資料庫的 Schema 元素 &#40;DTA&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>備註  
 在 Database Engine Tuning Advisor XML 結構描述中，這個元素的名稱為 **DatabaseDetailsTypecomplexType** 。 請勿混淆這個 `Database` 元素與根父系是 `Configuration` 元素的元素。 (請參閱[組態的 Database 元素 &#40;DTA&#41;](database-element-for-configuration-dta.md)。)  
  
## <a name="example"></a>範例  
 如需此`Database`元素的使用範例，請參閱[&#40;DTA&#41;的工作負載元素](workload-element-dta.md)中的程式碼範例。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
