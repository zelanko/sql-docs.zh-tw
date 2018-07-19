---
title: Isolation 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Isolation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Isolation element
ms.assetid: 28c98c6f-668e-4547-8d25-127cc3995a7d
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a21593d360342dc703e1da45d50b4ddff74241a7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37257224"
---
# <a name="isolation-element-assl"></a>Isolation 元素 (ASSL)
  指出衍生自元素的隔離等級[DataSource](../data-type/datasource-data-type-assl.md)資料型別。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataSource>  
   ...  
   <Isolation>...</Isolation>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*ReadCommitted*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DataSource](../data-type/datasource-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*ReadCommitted*|指定陳述式不能讀取其他交易已修改而尚未認可的資料。 這個選項可避免中途讀取。 其他交易可以變更目前交易內部個別陳述式之間的資料。 這會導致不可重複讀取或虛設項目資料。 此值為 `Isolation` 元素的預設值。|  
|*快照式*|指定交易中任何陳述式所讀取的資料，都是交易啟動時就存在之資料的交易一致性版本。 交易只能查看交易啟動之前所認可的資料修改。 其他交易在目前交易開始之後所做的資料修改將不會顯示給在目前交易中執行的陳述式。 結果是交易中的陳述式會取得已認可之資料的快照集，如同資料在交易啟動時的狀態。|  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
