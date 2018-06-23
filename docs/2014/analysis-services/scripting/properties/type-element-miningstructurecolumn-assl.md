---
title: 輸入元素 (MiningStructureColumn) (ASSL) |Microsoft 文件
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
- Type Element (MiningStructureColumn)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: ce999716-9487-4348-bc42-270a2026a452
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: bac190fcde3dfb4a5e0768e42c7cf0e1b7b6659f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135489"
---
# <a name="type-element-miningstructurecolumn-assl"></a>Type 元素 (MiningStructureColumn) (ASSL)
  包含的型別[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningStructureColumn>  
   ...  
   <Type>...</Type>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*Long*|64 位元帶正負號的整數。 這個資料類型會對應至 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 中的 `Int64` 資料類型和 OLE DB 中的 DBTYPE_I8 資料類型。|  
|*布林*|布林值。 這個資料類型會對應至 .NET Framework 中的 `Boolean` 資料類型和 OLE DB 中的 DBTYPE_BOOL 資料類型。|  
|*Text*|Unicode 字元的以 Null 結束資料流。 這個資料類型會對應至 .NET Framework 中的 `String` 資料類型和 OLE DB 中的 DBTYPE_WSTR 資料類型。|  
|*double*|在 -1.79E +308 到 1.79E +308 範圍中的雙精確度浮點數。 這個資料類型會對應至 .NET Framework 中的 `Double` 資料類型和 OLE DB 中的 DBTYPE_R8 資料類型。|  
|*日期*|儲存成雙精確度浮點數的日期資料。 整數部分為自 1899 年 12 月 30 日起的天數，而分數部分則為一天的分數部分。 這個資料類型會對應至 .NET Framework 中的 `DateTime` 資料類型和 OLE DB 中的 DBTYPE_DATE 資料類型。|  
|*[資料表]*|巢狀資料表。 這個資料類型會對應至 OLE DB 中的 DBTYPE_HCHAPTER 資料類型。 **注意：** .NET Framework 中的資料表資料行不具有對等的內建資料類型，但改為支援`DataReader`類別。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `Type` 允許值的列舉是 <xref:Microsoft.AnalysisServices.MiningStructureColumnTypes>。  
  
 對應目的父代的項目`Type`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.MiningStructureColumn>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  