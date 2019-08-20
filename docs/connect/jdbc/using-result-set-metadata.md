---
title: 使用結果集中繼資料 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ed0b1eedcafa1fab59d17f756523fc0fc189200
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026117"
---
# <a name="using-result-set-metadata"></a>使用結果集中繼資料

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

為了查詢結果集內所包含之資料行的資訊，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會實作 [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) 類別。 此類別包含數種以單一值形式傳回資訊的方法。

若要建立 SQLServerResultSetMetaData 物件, 您可以使用[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)類別的[getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)方法。

在下列範例中, 連至[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫的開啟連接會傳遞至函式中, SQLServerResultSet 類別的 getMetaData 方法會用來傳回 SQLServerResultSetMetaData 物件, 然後使用下列各項的方法:SQLServerResultSetMetaData 物件是用來顯示結果集內所包含之資料行的名稱和資料類型的相關資訊。

[!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]

## <a name="see-also"></a>另請參閱

[使用 JDBC 驅動程式處理中繼資料](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
