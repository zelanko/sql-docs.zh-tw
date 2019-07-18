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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 50476cb92d477bb9a72ac8d4311d24572b0368e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069677"
---
# <a name="gateways-diagnostic-example"></a>閘道診斷範例
在閘道架構中，驅動程式會將要求傳送至支援 ODBC 的閘道。 閘道會將要求傳送至 DBMS。 因為它是介面驅動程式管理員使用的元件時，驅動程式格式，並傳回引數**SQLGetDiagRec**。  
  
 例如，如果 Oracle Microsoft Open Data Services 和 Rdb 如果找不到資料表員工根據 Rdb 的閘道，閘道可能會產生此診斷訊息：  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 資料來源中發生錯誤，因為閘道會加入診斷訊息 ([Rdb]) 的資料來源識別碼的前置詞。 因為閘道所使用的資料來源的元件，它會加入至診斷訊息的前置詞，其供應商 ([DEC]) 和識別項 （[ODS 閘道]）。 它也會加入 SQLSTATE 值和 Rdb 錯誤程式碼的診斷訊息開頭。 這允許它保留它自己的訊息結構的語意，並仍提供驅動程式的 ODBC 診斷資訊。 驅動程式剖析透過閘道連接到的錯誤陳述式的錯誤資訊。  
  
 因為閘道驅動程式介面驅動程式管理員使用的元件，它會使用上述的診斷訊息來格式化，並傳回下列值從**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
