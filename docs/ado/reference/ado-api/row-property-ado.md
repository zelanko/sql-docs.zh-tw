---
title: Row 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::PutRow
- ADORecordConstruction::GetRow
- ADORecordConstruction::get_Row
- ADORecordConstruction::Row
- ADORecordConstruction::put_Row
helpviewer_keywords:
- Row property [ADO]
ms.assetid: 21019d89-2dd1-4a26-ac6f-384b81d66949
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 134f5fe05f89d6c8662a68f9f782f460c4b5f0aa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917108"
---
# <a name="row-property-ado"></a>Row 屬性 (ADO)
從或在[ADORecordConstruction 介面](../../../ado/reference/ado-api/adorecordconstruction-interface.md)物件上，取得或設定 OLE DB 的資料**列**物件。 當您使用**put_Row**設定資料**列**物件時，會將資料列轉換成 ADO**記錄**物件。  
  
## <a name="readwritesyntax"></a>讀取/寫入。語法  
  
```  
HRESULT get_Row([out, retval] IUnknown** ppRow);  
HRESULT put_Row([in] IUnknown* pRow);  
```  
  
## <a name="parameters"></a>參數  
 *ppRow*  
 OLE DB **Row**物件的指標。  
  
 *PRow*  
 OLE DB 的資料**列**物件。  
  
## <a name="return-values"></a>傳回值  
 這個屬性方法會傳回標準 HRESULT 值，包括 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>套用至  
 [ADORecordConstruction 介面](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
