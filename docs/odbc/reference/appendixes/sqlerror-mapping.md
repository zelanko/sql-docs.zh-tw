---
title: "SQLError 對應 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLError
- SQLError function [ODBC], mapping
ms.assetid: 802ac711-7e5d-4152-9698-db0cafcf6047
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7ebbe17713149276acbe061bfb8ba41503026306
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlerror-mapping"></a>SQLError 對應
當應用程式呼叫**SQLError**透過 ODBC 3*.x*驅動程式，會呼叫  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 對應到  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 與*HandleType*將設定為 SQL_HANDLE_ENV、 利用 SQL_HANDLE_DBC 或利用 SQL_HANDLE_STMT，視需要的引數和*處理*引數設定中的值為*henv*， *hdbc*，或*hstmt*視情況。 *RecNumber*引數的判斷，驅動程式管理員。
