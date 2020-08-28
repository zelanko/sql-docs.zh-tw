---
description: '使用 #import) ConnectionEvents (Visual C++ 語法索引'
title: '使用 #import) ConnectionEvents (Visual C++ 語法索引 |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- 'ConnectionEvents collection [ADO], Visual C++ syntax index with #import'
ms.assetid: dd052d36-7730-4400-822b-0544fb1992b4
author: rothja
ms.author: jroth
ms.openlocfilehash: 8ccd1f8de3a1ca2b5b44a32fa9e9d02f610abf53
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974809"
---
# <a name="connectionevents-visual-c-syntax-index-with-import"></a>使用 #import) ConnectionEvents (Visual C++ 語法索引
## <a name="events"></a>事件  
  
```  
HRESULT InfoMessage( struct Error * pError, enum  
    EventStatusEnum *     adStatus, struct _Connection * pConnection );  
  
HRESULT BeginTransComplete( long TransactionLevel,  
    struct Error * pError, enum EventStatusEnum * adStatus, struct  
    _Connection * pConnection );  
  
HRESULT CommitTransComplete( struct Error *  
    pError, enum EventStatusEnum     * adStatus, struct _Connection *  
    pConnection );  
  
HRESULT RollbackTransComplete( struct Error *  
    pError, enum     EventStatusEnum * adStatus, struct _Connection *  
    pConnection );  
  
HRESULT WillExecute( BSTR * Source, enum  
    CursorTypeEnum * CursorType,  
    enum LockTypeEnum * LockType, long * Options, enum EventStatusEnum *  
    adStatus, struct _Command * pCommand, struct _Recordset * pRecordset,  
    struct _Connection * pConnection );  
  
HRESULT ExecuteComplete( long RecordsAffected, struct  
    Error * pError,     enum EventStatusEnum * adStatus, struct _Command  
    * pCommand, struct     _Recordset * pRecordset, struct _Connection *  
    pConnection );  
  
HRESULT WillConnect( BSTR * ConnectionString, BSTR *  
    UserID, BSTR *     Password, long * Options, enum EventStatusEnum *  
    adStatus, struct     _Connection * pConnection );  
  
HRESULT ConnectComplete( struct Error *  
    pError, enum EventStatusEnum *     adStatus, struct _Connection *  
    pConnection );  
  
HRESULT Disconnect( enum EventStatusEnum *  
    adStatus, struct _Connection *     pConnection );  
```
