---
description: getCatalogs 方法 (SQLServerDatabaseMetaData)
title: getCatalogs 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCatalogs
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7f8bd0f1-f340-4bb9-b559-0a6176124033
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a31fca087c206104d197a3121db90991ff38f8c8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436900"
---
# <a name="getcatalogs-method-sqlserverdatabasemetadata"></a>getCatalogs 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取已連接伺服器中所提供的目錄名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getCatalogs()  
```  
  
## <a name="return-value"></a>傳回值  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此 getCatalogs 方法由 java.sql.DatabaseMetaData 介面中的 getCatalogs 方法所指定。  
  
> [!NOTE]  
>  在 Azure SQL Database 上，您應該連線至 master 資料庫來呼叫 **SQLServerDatabaseMetaData.getCatalogs**。 SQL Database 不支援從使用者資料庫傳回整組目錄。 **SQLServerDatabaseMetaData.getCatalogs** 會使用 sys.databases 檢視取得目錄。 請參閱 [sys.database_usage (Azure SQL Database)](../../../relational-databases/system-catalog-views/sys-database-usage-azure-sql-database.md) 中關於權限的討論，以了解 SQL 上的 **SQLServerDatabaseMetaData.getCatalogs** 行為。在 Azure SQL Database 上，您應該連線至 master 資料庫來呼叫 **SQLServerDatabaseMetaData.getCatalogs**。 SQL Database 不支援從使用者資料庫傳回整組目錄。 **SQLServerDatabaseMetaData.getCatalogs** 會使用 sys.databases 檢視取得目錄。 請參閱 [sys.database_usage (Azure SQL Database)](../../../relational-databases/system-catalog-views/sys-database-usage-azure-sql-database.md) 中關於權限的討論，以了解 SQL Database 上的 **SQLServerDatabaseMetaData.getCatalogs** 行為。                      .  
  
 getCatalogs 方法所傳回的結果集將包含下列資訊：  
  
|名稱|類型|描述|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|目錄名稱，包含 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的系統資料庫。|  
  
## <a name="example"></a>範例  
 下列範例會說明如何使用 getCatalogs 方法來傳回 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 內含之所有資料庫的名稱，包括系統資料庫。  
  
```  
public static void executeGetCatalogs(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getCatalogs();  
      ResultSetMetaData rsmd = rs.getMetaData();  
  
      // Display the result set data.  
      int cols = rsmd.getColumnCount();  
      while(rs.next()) {  
         for (int i = 1; i <= cols; i++) {  
            System.out.println(rs.getString(i));  
         }  
      }  
      rs.close();  
   }   
  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
