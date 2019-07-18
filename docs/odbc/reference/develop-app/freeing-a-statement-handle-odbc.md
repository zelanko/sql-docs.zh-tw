---
title: 釋放陳述式控制代碼 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 638cf9fb3c7af73130cf1413559b9baee2a354c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069784"
---
# <a name="freeing-a-statement-handle-odbc"></a>釋放陳述式控制代碼 ODBC
如先前所述，它是更有效率的方式重複使用比要卸除它們，並配置新的陳述式。 然後再執行新的 SQL 陳述式的陳述式，應用程式應該確定目前的陳述式設定適當。 這些包括陳述式屬性、參數繫結，以及結果集繫結。 一般而言，參數和結果集，舊的 SQL 陳述式需要將解除繫結 (藉由呼叫**SQLFreeStmt**使用 SQL_RESET_PARAMS 和 SQL_UNBIND 選項) 和重新繫結為新的 SQL 陳述式。  
  
 當應用程式完成使用陳述式時，它會呼叫**SQLFreeHandle**來釋放陳述式。 釋放陳述式，之後應用程式的程式設計錯誤的 ODBC 函式; 呼叫中使用的陳述式控制代碼如此一來，所以都未定義，但可能嚴重的後果。  
  
 當**SQLFreeHandle**呼叫時，驅動程式版本結構用來儲存有關陳述式的資訊。  
  
 **SQLDisconnect**自動釋放連接上的所有陳述式。
