---
title: 使用參數中繼資料 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: db2c1957-91c6-4989-a07b-9f8be6d2033a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54afa3bf0df1c0c4df3865ab28e7b085bb032919
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47623646"
---
# <a name="using-parameter-metadata"></a>使用參數中繼資料

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

若要查詢 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 或 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 物件有關其所包含的參數，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會實作 [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) 類別。 此類別包含以單一值格式傳回資訊的許多欄位與方法。

若要建立 SQLServerParameterMetaData 物件時，您可以使用[getParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) SQLServerPreparedStatement 和 SQLServerCallableStatement 類別的方法。

在下列範例中，開啟連線[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式、 SQLServerCallableStatement 類別的 getParameterMetaData 方法用來傳回 SQLServerParameterMetaData 物件，然後各種SQLServerParameterMetaData 物件的方法用來顯示資訊的類型和模式都包含在 HumanResources.uspUpdateEmployeeHireInfo 預存程序的參數。

[!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  

> [!NOTE]  
> SQLServerParameterMetaData 類別使用備妥的陳述式時，有一些限制。
>
> **使用 Microsoft JDBC Driver 6.0 (或更高版本) for SQL Server**：使用 SQL Server 2008 或 2008 R2 時，JDBC 驅動程式支援 SELECT、DELETE、INSERT 與 UPDATE 陳述式 (只要這些陳述式不包含子查詢及/或聯結)。

使用 SQL Server 2008 或 2008 R2 時，對 SQLServerParameterMetaData 類別也不支援 MERGE 查詢。 若是 SQL Server 2012 及更高版本，則支援具備複雜查詢的參數中繼資料。

不支援擷取加密的資料行的參數中繼資料。 **使用 Microsoft JDBC Driver 4.1 或 4.2 for SQL Server**：JDBC 驅動程式支援 SELECT、DELETE、INSERT 與 UPDATE 陳述式 (只要這些陳述式不包含子查詢及/或聯結)。 SQLServerParameterMetaData 類別也不支援合併查詢。
