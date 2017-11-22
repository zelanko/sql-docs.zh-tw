---
title: "資料列集屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADORecordsetConstruction::PutRowset
- ADORecordsetConstruction::GetRowset
- ADORecordsetConstruction::Rowset
- ADORecordsetConstruction::put_Rowset
- ADORecordsetConstruction::get_Rowset
helpviewer_keywords: Rowset property [ADO]
ms.assetid: 7d359294-4ff2-47e0-8111-0c221b24d80e
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8792f0b78e2dcc565d88847767506c310160ed5c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="rowset-property-ado"></a>資料列集屬性 (ADO)
取得或設定 OLE DB**資料列集**物件上從 / **ADORecordsetConstruction**物件。 當您使用 put_Rowset 時，資料列集就會轉換成 ADO**資料錄集**物件。  
  
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
 這個屬性的方法會傳回標準的 HRESULT 值，包括 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>適用於  
 [ADORecordsetConstruction 介面](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
