---
title: Rowset 屬性（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3eb383bb0e5cadf557ff67a1e97d1b6b5a6bf988
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82755999"
---
# <a name="rowset-property-ado"></a>Rowset 屬性 (ADO)
取得或設定**ADORecordsetConstruction**物件上/的 OLE DB 資料列**集**物件。 當您使用 put_Rowset 時，會將資料列集轉換成 ADO**記錄集**物件。  
  
 讀取/寫入  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT get_Rowset([out, retval] IUnknown** ppRowset);  
HRESULT put_Rowset([in] IUnknown* pRowset);  
```  
  
## <a name="parameters"></a>參數  
 *ppRowset*  
 OLE DB 資料列**集**物件的指標。  
  
 *PRowset*  
 OLE DB 的資料列**集**物件。  
  
## <a name="return-values"></a>傳回值  
 這個屬性方法會傳回標準 HRESULT 值，包括 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>套用至  
 [ADORecordsetConstruction 介面](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
