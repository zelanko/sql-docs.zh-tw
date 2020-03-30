---
title: 使用資料庫中繼資料 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fce2bf9d72136b303ee3bc974f3aede313233a82
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026424"
---
# <a name="using-database-metadata"></a>使用資料庫中繼資料

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

為了查詢資料庫中有關其支援之項目的資訊，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會實作 [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 類別。 此類別包含數種方法，會以單一值形式或以結果集傳回資訊。

若要建立 SQLServerDatabaseMetaData 物件，您可以使用 [SQLServerConnection](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) 類別的 [getMetaData](../../connect/jdbc/reference/sqlserverconnection-class.md) 方法來取得有關它連線之資料庫的資訊。

在下列範例中，針對 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的開啟連線會傳遞至函式中，並使用 SQLServerConnection 類別的 getMetaData 方法傳回 SQLServerDatabaseMetadata 物件，然後使用 SQLServerDatabaseMetaData 物件的各種方法來顯示有關驅動程式、驅動程式版本、資料庫名稱和資料庫版本的資訊。

[!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]

## <a name="see-also"></a>另請參閱

[使用 JDBC 驅動程式處理中繼資料](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
