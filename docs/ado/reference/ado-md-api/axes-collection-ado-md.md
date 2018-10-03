---
title: 軸集合 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axes
- Cellset::Axes
helpviewer_keywords:
- Axes collection [ADO MD]
ms.assetid: 072fb21a-ec0f-4b02-9022-1cef3ad4bfff
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bb700997165ceeb6d300f6332c9e758706c0fbc1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47630900"
---
# <a name="axes-collection-ado-md"></a>Axes 集合 (ADO MD)
包含[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)定義資料格集的物件。  
  
## <a name="remarks"></a>備註  
 A [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件包含**軸**集合。 一次**Cellset**已開啟，這個集合會包含至少一個**軸**。 請參閱[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)詳細說明如何使用的物件**軸**物件。  
  
> [!NOTE]
>  篩選座標軸**Cellset**並未包含在**軸**集合。 請參閱[FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md)屬性，如需詳細資訊。  
  
 **軸**是標準的 ADO 集合。 使用屬性和集合的方法，您可以執行下列作業：  
  
-   取得集合中具有的物件數目[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性。  
  
-   傳回集合中具有預設值的物件[項目](../../../ado/reference/ado-api/item-property-ado.md)屬性。  
  
-   更新的提供者從集合中的物件[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/axes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Cellset 範例 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Axis 物件 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)
