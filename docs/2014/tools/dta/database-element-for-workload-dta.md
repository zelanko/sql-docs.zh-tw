---
title: Database 元素 (DTA) 的工作負載 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 112fca2a-37e5-4162-b2e7-b56eb8ab0c6f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f3f5f7d912a41476588662c4543b20c041b02672
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172138"
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
|**出現次數**|如果未指定任何其他工作負載類型，便需要使用這個元素一次。 您必須指定`EventString`，則`File`，或有`Database`子元素`Workload`父代，但只有一個型別使用。 例如，如果您利用 `Database` 元素指定了工作負載，便不能在相同 XML 輸入檔中，同時利用 `File` 元素來指定工作負載。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[Workload 元素&#40;DTA&#41;](workload-element-dta.md)|  
|**子元素**|[資料庫的名稱項目&#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [資料庫的 schema 元素&#40;DTA&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>備註  
 在 Database Engine Tuning Advisor XML 結構描述中，這個元素的名稱為 **DatabaseDetailsTypecomplexType** 。 請勿混淆這個 `Database` 元素與根父系是 `Configuration` 元素的元素。 (請參閱[組態的 Database 元素 &#40;DTA&#41;](database-element-for-configuration-dta.md)。)  
  
## <a name="example"></a>範例  
 如需使用範例，這`Database`項目，請參閱中的程式碼範例[Workload 元素&#40;DTA&#41;](workload-element-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
