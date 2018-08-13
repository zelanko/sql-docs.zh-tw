---
title: 使用 SQL 陳述式搭配參數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3202b88f-ce13-44dd-982c-c6a3b0260378
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbbe0ff57b131cf3e7d3c943d72bdf34bdc4e4ce
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/08/2018
ms.locfileid: "39661690"
---
# <a name="using-an-sql-statement-with-parameters"></a>搭配參數使用 SQL 陳述式

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

若要使用包含 IN 參數的 SQL 陳述式，來使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 資料庫中的資料，您可以使用 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 類別的 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) 方法，以傳回將包含所要求資料的 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)。 若要這樣做，您必須先使用 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 類別的 [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) 方法建立 SQLServerPreparedStatement 物件。

當建構 SQL 陳述式時，請使用 ? (問號) 字元來指定 IN 參數，這個問號是作為預留位置，代表稍後將傳遞至 SQL 陳述式的參數值。 若要指定參數的值，您可以使用 SQLServerPreparedStatement 類別的 setter 方法的其中一個。 您使用的 setter 方法，是由要傳遞至 SQL 陳述式的值資料類型所決定。

當您將值傳遞至 setter 方法時，您不但要指定用於 SQL 陳述式的實際值，也要指定 SQL 陳述式中參數的序數位置。 例如，如果您的 SQL 陳述式包含單一參數，其序數值將會是 1。 如果陳述式包含兩個參數，則第一個序數值為 1，而第二個序數值會是 2。

在下列範例中，會將連至 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的開啟連線傳入至函式、建構 SQL 準備陳述式並使用單一 String 參數值執行，然後從結果集中讀取結果。

[!code[JDBC#UsingSQLWithParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_1_1.java)]

## <a name="see-also"></a>另請參閱

[搭配使用陳述式與 SQL](../../connect/jdbc/using-statements-with-sql.md)
