---
title: "屬性 (ADO) 資料列 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19b935d43739d1a1ce19f414cae12b00c311b261
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="row-property-ado"></a>資料列的屬性 (ADO)
取得或設定 OLE DB**列**物件上的往來[ADORecordConstruction 介面](../../../ado/reference/ado-api/adorecordconstruction-interface.md)物件。 當您使用**put_Row**設定**列**物件、 一個資料列會轉換成 ADO**記錄**物件。  
  
## <a name="readwritesyntax"></a>讀取/寫入。語法  
  
```  
HRESULT get_Row([out, retval] IUnknown** ppRow);  
HRESULT put_Row([in] IUnknown* pRow);  
```  
  
## <a name="parameters"></a>參數  
 *ppRow*  
 OLE DB 指標**列**物件。  
  
 *PRow*  
 OLE DB**列**物件。  
  
## <a name="return-values"></a>傳回值  
 這個屬性的方法會傳回標準的 HRESULT 值，包括 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>適用於  
 [ADORecordConstruction 介面](../../../ado/reference/ado-api/adorecordconstruction-interface.md)

