---
title: "使用參數中繼資料 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: db2c1957-91c6-4989-a07b-9f8be6d2033a
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d50af4d0d22d6042230fed2ee6b989fb7c53408d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="using-parameter-metadata"></a>使用參數中繼資料
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  要查詢[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)或[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)物件有關其所包含參數，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]實作[SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md)類別。 此類別包含以單一值格式傳回資訊的許多欄位與方法。  
  
 若要建立 SQLServerParameterMetaData 物件時，您可以使用[getParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) SQLServerPreparedStatement 和 SQLServerCallableStatement 類別的方法。  
  
 在下列範例中，開啟連接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式、 SQLServerCallableStatement 類別的 getParameterMetaData 方法用來傳回 SQLServerParameterMetaData 物件，然後各種SQLServerParameterMetaData 物件的方法用來顯示型別和 HumanResources.uspUpdateEmployeeHireInfo 預存程序內所包含的參數模式資訊。  
  
 [!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  
    
> [!NOTE]  
當使用 SQLServerParameterMetaData 類別搭配備妥的陳述式時，有一些限制。 
**Microsoft JDBC Driver 6.0 （或更高） for SQL Server**： 使用 SQL Server 2008 或 2008 R2 時，JDBC 驅動程式支援 SELECT、 DELETE、 INSERT 及 UPDATE 陳述式，只要這些陳述式不包含子查詢及/或聯結。 合併查詢也不支援對 SQLServerParameterMetaData 類別時使用 SQL Server 2008 或 2008 R2。 若是 SQL Server 2012 及更高版本，則支援具備複雜查詢的參數中繼資料。 不支援擷取加密的資料行的參數中繼資料。 **Microsoft JDBC Driver 4.0，4.1 或 4.2 for SQL Server 與**: JDBC 驅動程式支援 SELECT、 DELETE、 INSERT 及 UPDATE 陳述式，只要這些陳述式不包含子查詢及/或聯結。 SQLServerParameterMetaData 類別也不支援 MERGE 查詢。  

## <a name="see-also"></a>另請參閱  
 [JDBC driver 處理中繼資料](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  

