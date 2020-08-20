---
description: SQLError 對應
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
ms.openlocfilehash: 5d18d1b25acbbe56f29555274a7b8d995b7355d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466020"
---
# <a name="sqlerror-mapping"></a>SQLError 對應
當應用程式*透過 ODBC 3.x*驅動程式呼叫**SQLError**時，呼叫  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 對應至  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 將 *HandleType* 引數設定為值 SQL_HANDLE_ENV、SQL_HANDLE_DBC 或 SQL_HANDLE_STMT，適當地將 *控制碼* 引數設定為 *henv*、 *hdbc*或 *hstmt*中的值。 *RecNumber*引數是由驅動程式管理員所決定。
