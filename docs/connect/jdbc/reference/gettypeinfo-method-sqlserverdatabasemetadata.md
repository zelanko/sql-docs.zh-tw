---
title: getTypeInfo 方法 (SQLServerDatabaseMetaData) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getTypeInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 23208f01-c1bf-4235-b29c-9051d3df59a3
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 032ddf6a5f266fa68c6a735dd7f59cf4df02c68e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="gettypeinfo-method-sqlserverdatabasemetadata"></a>getTypeInfo 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前資料庫支援之所有標準 SQL 類型的描述。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getTypeInfo()  
```  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getTypeInfo 方法是由 java.sql.DatabaseMetaData 介面中 getTypeInfo 方法指定。  
  
 GetTypeInfo 方法所傳回的結果集將包含下列資訊：  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|TYPE_NAME|**字串**|資料類型的名稱。|  
|DATA_TYPE|**short**|來自 java.sql.Types 的 SQL 資料型別。|  
|PRECISION|**int**|有效位數的總數。|  
|LITERAL_PREFIX|**字串**|用於常數前面的字元或多個字元。|  
|LITERAL_SUFFIX|**字串**|用於中止常數的字元或多個字元。|  
|CREATE_PARAMS|**字串**|資料類型之 creation 參數的描述。|  
|NULLABLE|**short**|指出資料行是否能包含 null 值。 它可能是下列其中一個值：<br /><br /> typeNoNulls (0)<br /><br /> typeNullable (1)<br /><br /> typeNullableUnknown (2)|  
|CASE_SENSITIVE|**boolean**|指出資料類型是否區分大小寫。 「**true**"如果類型是區分大小寫，否則 「**false**"。|  
|SEARCHABLE|**short**|指出資料行是否能用於 SQL WHERE 子句。 它可能是下列其中一個值：<br /><br /> typePredNone (0)<br /><br /> typePredChar (1)<br /><br /> typePredBasic (2)<br /><br /> typeSeachable (3)|  
|UNSIGNED_ATTRIBUTE|**boolean**|指出資料類型的正負號。 「**true**"如果類型是不帶正負號; 否則 「**false**"。|  
|FIXED_PREC_SCALE|**boolean**|指出資料類型可以是 money 值。 "**true**"如果資料類型為 money 類型，否則"**false**"。|  
|AUTO_INCREMENT|**boolean**|指出資料類型可以自動遞增。 「**true**"if 類型可以自動遞增，否則 「**false**"。|  
|LOCAL_TYPE_NAME|**字串**|資料類型的當地語系化名稱。|  
|MINIMUM_SCALE|**short**|小數點右邊的最大位數。|  
|MAXIMUM_SCALE|**short**|小數點右邊的最小位數。|  
|SQL_DATA_TYPE|**int**|JDBC 驅動程式不支援。|  
|SQL_DATETIME_SUB|**int**|JDBC 驅動程式不支援。|  
|NUM_PREC_RADIX|**int**|用來計算資料行可保留之最大數字的位元數目或位數。|  
|INTERVAL_PRECISION|**smallint**|間隔開頭有效位數的值。|  
|USERTYPE|**smallint**|**Usertype**值**systypes**資料表。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 線上叢書》。|  
  
> [!NOTE]  
>  多個 getTypeInfo 方法所傳回的資料的詳細資訊，請參閱 「 sp_datatype_info (TRANSACT-SQL) 」，在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 getTypeInfo 方法來傳回使用中的資料類型的相關資訊[!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)]（或更新版本） 資料庫。  
  
```  
public static void executeGetTypeInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTypeInfo();  
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
  
  
