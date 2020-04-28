---
title: 閘道診斷範例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], examples
- gateway diagnostic [ODBC]
- error messages [ODBC], diagnostic messages
ms.assetid: e0695fac-4593-4b3d-8675-cb8f73dab966
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b18fd78be7be2eb79316339cbdf3d315deb194fb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305569"
---
# <a name="gateways-diagnostic-example"></a>閘道診斷範例
在閘道架構中，驅動程式會將要求傳送至支援 ODBC 的閘道。 閘道會將要求傳送至 DBMS。 由於它是與驅動程式管理員介面的元件，因此驅動程式會格式化並傳回**SQLGetDiagRec**的引數。  
  
 例如，如果以 Oracle 為基礎的閘道在 Microsoft Open 資料服務上為 Rdb，而如果 Rdb 找不到資料表 EMPLOYEE，閘道可能會產生此診斷訊息：  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 因為此錯誤發生在資料來源中，所以閘道會將資料來源識別碼（[Rdb]）的前置詞加入至診斷訊息。 因為閘道是與資料來源介面的元件，所以它會將其廠商的首碼（[DEC]）和識別碼（[ODS 閘道]）新增至診斷訊息。 它也會將 SQLSTATE 值和 Rdb 錯誤碼加入至診斷訊息的開頭。 這允許它保留自己的訊息結構的語義，並仍然提供 ODBC 診斷資訊給驅動程式。 驅動程式會剖析閘道附加至 error 語句的錯誤資訊。  
  
 因為閘道驅動程式是與驅動程式管理員介面的元件，所以它會使用上述的診斷訊息來格式化，並從**SQLGetDiagRec**傳回下列值：  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
