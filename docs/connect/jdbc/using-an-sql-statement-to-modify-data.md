---
title: 使用 SQL 語句修改資料 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cbcdf01eed0114e1788f23cec3a24cf4a69329e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004020"
---
# <a name="using-an-sql-statement-to-modify-data"></a>使用 SQL 陳述式修改資料

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

若要使用 SQL 陳述式修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中包含的資料，您可以使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 類別的 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) 方法。 executeUpdate 方法會將 SQL 陳述式傳遞至資料庫以進行處理，然後傳回值以指出受影響的資料列數目。

若要這樣做，您必須先使用 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 類別的 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 方法建立 SQLServerStatement 物件。

在下列範例中，[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的開啟連線會傳入至函式、建構一個將新資料新增至資料表的 SQL 陳述式，然後執行陳述式並顯示傳回值。

[!code[JDBC#UsingSQLToModifyData1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_1_1.java)]

> [!NOTE]  
> 如果必須使用含有參數的 SQL 陳述式來修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料，應該使用 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 類別的 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md) 方法。
>
> 如果您嘗試要插入資料的資料行包含特殊字元 (例如空格)，則需提供要插入的值，即使這些值是預設值也一樣。 如果沒有提供，插入作業將失敗。
>
> 如果想要 JDBC 驅動程式傳回所有更新計數 (包括任何可能已引發之觸發程序所傳回的更新計數)，請將 lastUpdateCount 連接字串屬性設為 "false"。 如需 lastUpdateCount 屬性的詳細資訊, 請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。

## <a name="see-also"></a>另請參閱

[搭配使用陳述式與 SQL](../../connect/jdbc/using-statements-with-sql.md)
