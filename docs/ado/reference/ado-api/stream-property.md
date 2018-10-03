---
title: Stream 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction::GetStream
- ADOStreamConstruction::PutStream
- ADOStreamConstruction::put_Stream
- ADOStreamConstruction::Stream
- ADOStreamConstruction::get_Stream
helpviewer_keywords:
- Stream property
ms.assetid: 4a44f9f6-0265-4c00-8def-d85b6af923b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ddeaadb1f25c3ea50e59c20d48f14e31831f2639
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822010"
---
# <a name="stream-property"></a>Stream 屬性
取得或設定 OLE DB **Stream**物件上的往返**ADOStreamConstruction**物件。  
  
 讀取/寫入  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>參數  
 *ppStream*  
 OLE DB 指標**Stream**物件。  
  
 *pStream*  
 OLE DB **Stream**物件。  
  
## <a name="return-values"></a>傳回值  
 此屬性的方法會傳回標準的 HRESULT 值。 這包括 S_OK 以及 E_FAIL。  
  
## <a name="applies-to"></a>適用於  
 [ADOStreamConstruction 介面](../../../ado/reference/ado-api/adostreamconstruction-interface.md)
