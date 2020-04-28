---
title: SQLError 對應 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLError
- SQLError function [ODBC], mapping
ms.assetid: 802ac711-7e5d-4152-9698-db0cafcf6047
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1aa3b66b29af755099cb273f3a19ca4e8230cd0b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302071"
---
# <a name="sqlerror-mapping"></a>SQLError 對應
當應用程式*透過 ODBC 3.x 驅動程式呼叫* **SQLError**時，呼叫  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 對應至  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 視情況，將*HandleType*引數設定為 SQL_HANDLE_ENV、SQL_HANDLE_DBC 或 SQL_HANDLE_STMT 的值，並適當地將*HANDLE*引數設定為*henv*、 *hdbc*或*hstmt*中的值。 *RecNumber*引數是由驅動程式管理員所決定。
