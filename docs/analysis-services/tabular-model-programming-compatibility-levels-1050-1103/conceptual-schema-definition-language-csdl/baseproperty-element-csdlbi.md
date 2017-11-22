---
title: "BaseProperty 元素 (CSDLBI) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: d0f63e52-7330-4b2c-a929-7a517acc6921
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 79d391ef3ac0388187c91dac96859172a347effc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="baseproperty-element-csdlbi"></a>BaseProperty 元素 (CSDLBI)
  BaseProperty 元素為複雜類型，可做為其他元素的基底。  
  
 其屬性可以出現在資料行和量值中。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 BaseProperty 元素的元素和屬性。  
  
|名稱|是否必要|說明|  
|----------|-----------------|-----------------|  
|Alignment|否|成員 (資料行、量值、導覽屬性、階層或層級) 的名稱，藉由實作 Member 類型所定義。|  
|FormatString|否|成員的顯示名稱。|  
|IsRightToLeft|否|布林值，指出欄位是否包含可由右至左讀取的文字。<br /><br /> 如果省略此屬性，則會使用 (模型的) 預設設定。|  
|SortDirection|否|值，指出一般的欄位值排序方式。 此屬性的內容是由 SortDirection 簡單類型定義。<br /><br /> 如果省略此屬性，排序方向是依據欄位的資料類型指派。|  
|單位|否|套用至欄位值以表示單位的符號。<br /><br /> 如果省略，則單位為未知。|  
  
## <a name="alignment-element"></a>Alignment 元素  
 此簡單類型會定義用於區分成員的命名格式。  
  
|Value|說明|  
|-----------|-----------------|  
|無|使用屬性名稱。|  
|內容|使用內送關聯性名稱。|  
|合併式|根據目前文法的規則，串連內送關聯性名稱和屬性名稱。|  
  
## <a name="sortdirection-element"></a>SortDirection 元素  
 此簡單類型會定義用於區分成員的命名格式。  
  
|Value|說明|  
|-----------|-----------------|  
|無|使用屬性名稱。|  
|內容|使用內送關聯性名稱。|  
|合併式|串連內送關聯性名稱和屬性名稱。|  
  
## <a name="see-also"></a>請參閱＜  
 [了解表格式物件模型在相容性層級 1050年透過 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
