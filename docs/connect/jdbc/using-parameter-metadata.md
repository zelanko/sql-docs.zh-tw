---
title: 使用參數中繼資料 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: db2c1957-91c6-4989-a07b-9f8be6d2033a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80ff8cebcc4141e8363c25f83821cb4924e6c46a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026079"
---
# <a name="using-parameter-metadata"></a>使用參數中繼資料

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

若要查詢 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 或 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 物件有關其所包含的參數，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會實作 [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) 類別。 此類別包含以單一值格式傳回資訊的許多欄位與方法。

若要建立 SQLServerParameterMetaData 物件，您可以使用 SQLServerPreparedStatement 與 SQLServerCallableStatement 類別的 [getParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) 方法。

在下列範例中，對 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的已開啟連線會傳遞至函式中，SQLServerCallableStatement 類別的 getParameterMetaData 方法會用來傳回 SQLServerParameterMetaData 物件，然後使用 SQLServerParameterMetaData 物件的各種方法來顯示 HumanResources.uspUpdateEmployeeHireInfo 預存程序內所包含參數之類型與模式的相關資訊。

[!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  

> [!NOTE]  
> 搭配備妥的陳述式使用 SQLServerParameterMetaData 類別時有一些限制。
>
> **使用適用於 SQL Server 的 Microsoft JDBC Driver 6.0 (或更新版本)** ：使用 SQL Server 2008 或 2008 R2 時，JDBC 驅動程式支援 SELECT、DELETE、INSERT 與 UPDATE 陳述式 (只要這些陳述式不包含子查詢和/或聯結)。

使用 SQL Server 2008 或 2008 R2 時，對 SQLServerParameterMetaData 類別也不支援 MERGE 查詢。 若是 SQL Server 2012 及更高版本，則支援具備複雜查詢的參數中繼資料。

不支援擷取加密資料行的參數中繼資料。 **使用適用於 SQL Server 的 Microsoft JDBC Driver 4.1 或 4.2**：JDBC 驅動程式支援 SELECT、DELETE、INSERT 與 UPDATE 陳述式 (只要這些陳述式不包含子查詢和/或聯結)。 SQLServerParameterMetaData 類別也不支援 MERGE 查詢。
