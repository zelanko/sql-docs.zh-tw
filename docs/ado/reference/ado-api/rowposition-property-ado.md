---
title: RowPosition 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::put_RowPosition
- ADORecordConstruction::PutRowPosition
- ADORecordConstruction::GetRowPosition
- ADORecordConstruction::RowPosition
- ADORecordConstruction::get_RowPosition
helpviewer_keywords:
- RowPosition property [ADO]
ms.assetid: 9d068fed-39bf-4842-afc3-686a2af2145d
author: rothja
ms.author: jroth
ms.openlocfilehash: f2621e82fef8d7e9baffa9d6cc8c30c65ea476ea
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82756203"
---
# <a name="rowposition-property-ado"></a>RowPosition 屬性 (ADO)
取得或設定在**ADORecordsetConstruction**物件上/的 OLE DB **RowPosition**物件。 當您使用**put_RowPosition**設定**RowPosition**物件時，產生的**記錄集**物件會使用**RowPosition**物件來判斷目前的資料列。  
  
 讀取/寫入  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT get_RowPosition([out, retval] IUnknown** ppRowPos);  
HRESULT put_RowPosition([in] IUnknown* pRowPos);  
```  
  
## <a name="parameters"></a>參數  
 *ppRowPos*  
 OLE DB **RowPosition**物件的指標。  
  
 *PRowPos*  
 OLE DB **RowPosition**物件。  
  
## <a name="return-values"></a>傳回值  
 這個屬性方法會傳回標準 HRESULT 值，包括 S_OK 和 E_FAIL。  
  
## <a name="remarks"></a>備註  
 當設定這個屬性時，如果**RowPosition**物件上的資料列**集**物件與**記錄集**物件**上的資料列集物件**不同，前者會覆寫後者。 相同的行為也適用于**RowPosition**的目前**章節**。  
  
## <a name="applies-to"></a>套用至  
 [ADORecordsetConstruction 介面](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
