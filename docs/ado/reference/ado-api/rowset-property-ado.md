---
title: 資料列集屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::PutRowset
- ADORecordsetConstruction::GetRowset
- ADORecordsetConstruction::Rowset
- ADORecordsetConstruction::put_Rowset
- ADORecordsetConstruction::get_Rowset
helpviewer_keywords:
- Rowset property [ADO]
ms.assetid: 7d359294-4ff2-47e0-8111-0c221b24d80e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f528ef5c83f0a9922c32fb06955d0ff921bfae6c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711432"
---
# <a name="rowset-property-ado"></a>Rowset 屬性 (ADO)
取得或設定 OLE DB**資料列集**物件上的往返**ADORecordsetConstruction**物件。 當您使用 put_Rowset 時，要將資料列集轉換成 ADO**資料錄集**物件。  
  
 讀取/寫入  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT get_Rowset([out, retval] IUnknown** ppRowset);  
HRESULT put_Rowset([in] IUnknown* pRowset);  
```  
  
## <a name="parameters"></a>參數  
 *ppRowset*  
 OLE DB 指標**資料列集**物件。  
  
 *PRowset*  
 OLE DB**資料列集**物件。  
  
## <a name="return-values"></a>傳回值  
 此屬性的方法會傳回標準的 HRESULT 值，包括 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>適用於  
 [ADORecordsetConstruction 介面](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
