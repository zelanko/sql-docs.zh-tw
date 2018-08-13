---
title: 使用 SQL 陳述式不含參數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4b0728bd-059b-4b71-895c-999335bc7427
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce923add20ff96ea63caea0073c5cfb9c6235253
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/08/2018
ms.locfileid: "39661680"
---
# <a name="using-an-sql-statement-with-no-parameters"></a>使用不含參數的 SQL 陳述式

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

若要使用不含參數的 SQL 陳述式來使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 資料庫中的資料，您可以使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 類別的 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 方法，來傳回一個將包含所要求之資料的 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)。 若要這樣做，您必須先使用 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 類別的 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 方法建立 SQLServerStatement 物件。

在下列範例中，連至 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的開啟連線會傳入至函式中，並建構及執行 SQL 陳述式，然後從結果集讀取結果。

[!code[JDBC#UsingSQLWithNoParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_0_1.java)]

如需使用結果集的詳細資訊，請參閱[JDBC driver 管理結果集](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)。

## <a name="see-also"></a>另請參閱

[搭配使用陳述式與 SQL](../../connect/jdbc/using-statements-with-sql.md)
