---
title: getTableTypes 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTableTypes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0f5dc57-07b8-4811-ab1a-80a524bfdb42
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8da791a53d6ee25dd56f7f015ccc69947999f3b9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67979153"
---
# <a name="gettabletypes-method-sqlserverdatabasemetadata"></a>getTableTypes 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前資料庫中所提供的資料表類型。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getTableTypes()  
```  
  
## <a name="return-value"></a>傳回值  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getTableTypes 方法是由 java.sql.DatabaseMetaData 介面中的 getTableTypes 方法指定。  
  
 透過 getTableTypes 方法所傳回的結果將包含下列資訊：  
  
|名稱|類型|描述|  
|----------|----------|-----------------|  
|TABLE_TYPE|**String**|資料表類型。|  
  
> [!NOTE]  
>  如需 getTableTypes 方法所傳回資料的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》中的＜sp_tables (Transact-SQL)＞。  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 getTableTypes 方法來傳回 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 範例資料庫中的資料表類型資訊 (假設連接字串中指定了資料庫)。  
  
```  
public static void executeGetTableTypes(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTableTypes();  
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
  
  
