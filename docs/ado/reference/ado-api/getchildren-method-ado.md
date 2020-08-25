---
description: GetChildren 方法 (ADO)
title: " (ADO) 的 GetChildren 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords:
- GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
author: rothja
ms.author: jroth
ms.openlocfilehash: d5d0ff58401e5294080c762c1e27f018630364f4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775097"
---
# <a name="getchildren-method-ado"></a>GetChildren 方法 (ADO)
傳回 [記錄集](./recordset-object-ado.md) ，其資料列代表集合 [記錄](./record-object-ado.md)的子系。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>傳回值  
 **記錄集**物件，其中每個資料列都代表目前**記錄**物件的子系。 例如，代表目錄之 **記錄** 的子系會是包含在上層目錄中的檔案和子目錄。  
  
## <a name="remarks"></a>備註  
 此提供者會決定哪些資料行存在於傳回的 **記錄集中**。 例如，檔來源提供者一律會傳回資源 **記錄集**。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Record 物件 (ADO)](./record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Recordset 物件 (ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::