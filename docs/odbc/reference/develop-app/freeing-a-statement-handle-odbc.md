---
title: "釋放陳述式控制代碼 ODBC |Microsoft 文件"
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
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b33d262c846d9ef8a41bf9440802664ac7d4b75f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="freeing-a-statement-handle-odbc"></a>釋放陳述式控制代碼 ODBC
如先前所述，會重複使用比卸除它們並配置新的陳述式更有效率。 然後再執行新的 SQL 陳述式的陳述式，應該確定目前的陳述式設定適合應用程式。 這些包括陳述式屬性、參數繫結，以及結果集繫結。 一般來說，參數和舊的 SQL 陳述式的結果集必須為未繫結 (藉由呼叫**SQLFreeStmt** SQL_RESET_PARAMS 和 SQL_UNBIND 選項) 和重新繫結為新的 SQL 陳述式。  
  
 當應用程式已經完成使用此陳述式時，它會呼叫**SQLFreeHandle**來釋放陳述式。 釋放後，陳述式，它是應用程式的程式設計錯誤; ODBC 函數呼叫中使用的陳述式控制代碼這樣做，因此必須未定義，但可能是嚴重的後果。  
  
 當**SQLFreeHandle**呼叫時，結構用來儲存資訊有關陳述式的驅動程式版本。  
  
 **SQLDisconnect**自動釋放連接上的所有陳述式。
