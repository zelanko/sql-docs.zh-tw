---
title: 釋放語句控制碼 ODBC |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069784"
---
# <a name="freeing-a-statement-handle-odbc"></a>釋放陳述式控制代碼 ODBC
如先前所述，重複使用語句比卸載它們並配置新的更有效率。 在語句上執行新的 SQL 語句之前，應用程式應該確定目前的語句設定是適當的。 這些包括陳述式屬性、參數繫結，以及結果集繫結。 一般來說，舊 SQL 語句的參數和結果集必須是未系結的（藉由使用 SQL_RESET_PARAMS 和 SQL_UNBIND 選項呼叫**SQLFreeStmt** ），然後重新系結新的 sql 語句。  
  
 當應用程式完成使用語句時，它會呼叫**SQLFreeHandle**來釋放語句。 釋放語句之後，應用程式設計錯誤會在 ODBC 函數的呼叫中使用語句的控制碼;這麼做並沒有定義，但可能會產生嚴重的後果。  
  
 呼叫**SQLFreeHandle**時，驅動程式會釋放用來儲存語句相關資訊的結構。  
  
 **SQLDisconnect**會自動釋放連接上的所有語句。
