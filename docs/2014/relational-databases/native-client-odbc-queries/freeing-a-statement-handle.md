---
title: 釋放陳述式控制代碼 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7da2fec15303e9c2d50fb7aa2e6dc40266a380d9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132640"
---
# <a name="freeing-a-statement-handle"></a>釋放陳述式控制代碼
  重複使用陳述式控制代碼比卸除陳述式控制代碼然後再配置新的陳述式控制代碼更有效率。 針對陳述式控制代碼執行新的 SQL 陳述式之前，應用程式應該確認目前的陳述式設定是否恰當。 這些包括陳述式屬性、參數繫結，以及結果集繫結。 一般來說，參數和結果集的舊的 SQL 陳述式必須藉由呼叫未繫結[SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md)利用 SQL_RESET_PARAMS 和 SQL_UNBIND 選項，並重新繫結為新的 SQL 陳述式。  
  
 當應用程式已經完成使用此陳述式時，它會呼叫[SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md)來釋放陳述式。 請注意， **SQLDisconnect**自動釋放連接上的所有陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [執行查詢&#40;ODBC&#41;](executing-queries-odbc.md)  
  
  