---
title: 閘道診斷範例 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], examples
- gateway diagnostic [ODBC]
- error messages [ODBC], diagnostic messages
ms.assetid: e0695fac-4593-4b3d-8675-cb8f73dab966
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9d77f42b0941cecc8a17fe3b54ee91705af0666
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="gateways-diagnostic-example"></a>閘道診斷範例
在閘道架構中，驅動程式會將要求傳送到支援 ODBC 的閘道。 閘道會將要求傳送至 DBMS。 因為它是介面的驅動程式管理員元件，驅動程式格式，並傳回引數**SQLGetDiagRec**。  
  
 例如，如果 Oracle 為基礎的閘道，Rdb Microsoft Open Data Services 和 Rdb 如果找不到員工資料表上，閘道器可能會產生此診斷訊息：  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 資料來源中發生錯誤，因為閘道會加入診斷訊息 ([Rdb]) 的資料來源識別碼的前置詞。 因為閘道 interfaced 與資料來源的元件，它會加入至診斷訊息的前置詞做為供應商 （[十進位]），並識別項 （[ODS 閘道]）。 它也會加入 SQLSTATE 值和 Rdb 錯誤程式碼的診斷訊息開頭。 這允許它以保留其本身的訊息結構的語意，並仍然提供驅動程式的 ODBC 診斷資訊。 驅動程式會剖析透過閘道連接到錯誤的陳述式的錯誤資訊。  
  
 因為閘道驅動程式介面的驅動程式管理員元件，它會使用上述的診斷訊息格式化，並傳回下列值從**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
