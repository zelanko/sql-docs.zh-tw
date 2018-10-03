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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a278609ee53fe7898d32c1986da2650202b8a98
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47719206"
---
# <a name="sqlerror-mapping"></a>SQLError 對應
當應用程式呼叫**SQLError**透過 ODBC 3 *.x*驅動程式，會呼叫  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 對應至  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 具有*HandleType*將設定為 SQL_HANDLE_ENV、 利用 SQL_HANDLE_DBC 或利用 SQL_HANDLE_STMT，視需要的引數和*處理*引數設定中的值為*henv*， *hdbc*，或*hstmt*視需要。 *RecNumber*引數的判斷，驅動程式管理員。
