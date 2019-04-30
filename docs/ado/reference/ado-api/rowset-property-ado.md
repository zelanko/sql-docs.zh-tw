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
manager: craigg
ms.openlocfilehash: 4bb98bb7c23d20baf696c553a088cd03f2aa76e1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63315790"
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
