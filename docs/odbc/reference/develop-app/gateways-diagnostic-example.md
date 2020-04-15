---
title: 閘道診斷範例 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305569"
---
# <a name="gateways-diagnostic-example"></a>閘道診斷範例
在閘道架構結構中,驅動程式將請求發送到支援ODBC的閘道。 閘道將請求發送到 DBMS。 因為它是與驅動程式管理器介面的元件,因此驅動程式格式並返回**SQLGetDiagRec**的參數。  
  
 例如,如果 Oracle 在 Microsoft 開放資料服務上基於 Rdb 的閘道,並且 Rdb 找不到表 EMPLOYEE,則閘道可能會生成此診斷訊息:  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 由於錯誤發生在數據源中,閘道向診斷消息添加了資料源標識符 ([Rdb]) 的前置碼。 由於閘道是與資料源介面的元件,因此它將供應商 ([DEC]) 和識別碼 ([ODS 閘道]) 的前置碼加入到診斷訊息中。 它還將 SQLSTATE 值和 Rdb 錯誤代碼添加到診斷消息的開頭。 這允許它保留其自己的消息結構的語義,並且仍然向驅動程式提供ODBC診斷資訊。 驅動程式解析閘道附加到錯誤語句的錯誤資訊。  
  
 由於閘道驅動程式是與驅動程式管理員介面的元件,它會使用前面的診斷訊息格式化並從**SQLGetDiagRec 傳回**以下值 :  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
