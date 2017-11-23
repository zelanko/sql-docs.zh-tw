---
title: "資料流屬性 |Microsoft 文件"
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
- ADOStreamConstruction::GetStream
- ADOStreamConstruction::PutStream
- ADOStreamConstruction::put_Stream
- ADOStreamConstruction::Stream
- ADOStreamConstruction::get_Stream
helpviewer_keywords: Stream property
ms.assetid: 4a44f9f6-0265-4c00-8def-d85b6af923b1
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6d55d9d2619f3739db97570e8195c7a199425252
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="stream-property"></a>資料流內容
取得或設定 OLE DB**資料流**物件上從 / **ADOStreamConstruction**物件。  
  
 讀取/寫入  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>參數  
 *ppStream*  
 OLE DB 指標**資料流**物件。  
  
 *pStream*  
 OLE DB**資料流**物件。  
  
## <a name="return-values"></a>傳回值  
 這個屬性的方法會傳回標準的 HRESULT 值。 這包括 S_OK 以及 E_FAIL。  
  
## <a name="applies-to"></a>適用於  
 [ADOStreamConstruction 介面](../../../ado/reference/ado-api/adostreamconstruction-interface.md)
