---
title: getBestRowIdentifier 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getBestRowIdentifier
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c19e9ca6-2a53-4a0c-91ab-80090c3f7229
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9a19bd01a8ebf54eb3e819bd4a82400b8107e382
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954020"
---
# <a name="getbestrowidentifier-method-sqlserverdatabasemetadata"></a>getBestRowIdentifier 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取資料表中最佳資料行集的描述，此資料行集可唯一識別資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getBestRowIdentifier(java.lang.String catalog,  
                                               java.lang.String schema,  
                                               java.lang.String table,  
                                               int scope,  
                                               boolean nullable)  
```  
  
#### <a name="parameters"></a>參數  
 *catalog*  
  
 包含目錄名稱的 **String**。  
  
 *schema*  
  
 包含結構描述名稱的 **String**。  
  
 *table*  
  
 包含資料表名稱的 **String**。  
  
 *範圍 (scope)*  
  
 **int**，指出感興趣的範圍。 可能的值如下：  
  
 bestRowTemporary (0)  
  
 bestRowTransaction (1)  
  
 bestRowSession (2)  
  
 *nullable*  
  
 **true** 表示包含可為 Null 的資料行。 否則為 **false**。  
  
## <a name="return-value"></a>傳回值  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getBestRowIdentifier 方法是由 JAVA.sql.databasemetadata 介面中的 getBestRowIdentifier 方法指定。  
  
 getBestRowIdentifier 方法所傳回的結果集將包含下列資訊：  
  
|[屬性]|類型|Description|  
|----------|----------|-----------------|  
|SCOPE|short|傳回之結果的範圍。 它可能是下列其中一個值：<br /><br /> bestRowTemporary (0)<br /><br /> bestRowTransaction (1)<br /><br /> bestRowSession (2)|  
|COLUMN_NAME|String|資料行的名稱。|  
|DATA_TYPE|short|來自 java.sql.Types 的 SQL 資料型別。|  
|TYPE_NAME|String|資料類型的名稱。|  
|COLUMN_SIZE|INT|資料行的有效位數。|  
|BUFFER_LENGTH|INT|緩衝區長度。|  
|DECIMAL_DIGITS|short|資料行的小數位數。|  
|PSEUDO_COLUMN|short|指出資料行是否為虛擬資料行。 它可能是下列其中一個值：<br /><br /> bestRowUnknown (0)<br /><br /> bestRowNotPseudo (1)<br /><br /> bestRowPseudo (2)|  
  
## <a name="example"></a>範例  
 下面範例示範如何使用 getBestRowIdentifier 方法來傳回 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 範例資料庫內 Person.Contact 資料表中最佳資料列識別碼的相關資訊。  
  
```  
public static void executeGetBestRowIdentifier(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getBestRowIdentifier(null, "Person", "Contact", 0, true);  
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
  
  
