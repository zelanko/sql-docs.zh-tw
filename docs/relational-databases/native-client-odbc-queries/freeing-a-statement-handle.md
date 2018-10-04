---
title: 釋放陳述式控制代碼 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1c28f3ba81ffbe346572dfba92adb31a7f198af9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47598696"
---
# <a name="freeing-a-statement-handle"></a>釋放陳述式控制代碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  重複使用陳述式控制代碼比卸除陳述式控制代碼然後再配置新的陳述式控制代碼更有效率。 針對陳述式控制代碼執行新的 SQL 陳述式之前，應用程式應該確認目前的陳述式設定是否恰當。 這些包括陳述式屬性、參數繫結，以及結果集繫結。 一般而言，參數和結果集的舊的 SQL 陳述式必須藉由呼叫未繫結[SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md)利用 SQL_RESET_PARAMS 和 SQL_UNBIND 選項，並重新繫結為新的 SQL 陳述式。  
  
 當應用程式完成使用陳述式時，它會呼叫[SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)來釋放陳述式。 請注意， **SQLDisconnect**自動釋放連接上的所有陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [執行查詢&#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
