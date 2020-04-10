---
title: getTypeInfo 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTypeInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 23208f01-c1bf-4235-b29c-9051d3df59a3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b007e5db3358cd1af350ac0d87af7df1af18518
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80911184"
---
# <a name="gettypeinfo-method-sqlserverdatabasemetadata"></a>getTypeInfo 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前資料庫支援之所有標準 SQL 類型的描述。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getTypeInfo()  
```  
  
## <a name="return-value"></a>傳回值  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getTypeInfo 方法是由 java.sql.DatabaseMetaData 介面中的 getTypeInfo 方法指定。  
  
 getTypeInfo 方法所傳回的結果將包含下列資訊：  
  
|名稱|類型|描述|  
|----------|----------|-----------------|  
|TYPE_NAME|**String**|資料類型的名稱。|  
|DATA_TYPE|**short**|來自 java.sql.Types 的 SQL 資料型別。|  
|PRECISION|**int**|有效位數的總數。|  
|LITERAL_PREFIX|**String**|用於常數前面的字元或多個字元。|  
|LITERAL_SUFFIX|**String**|用於中止常數的字元或多個字元。|  
|CREATE_PARAMS|**String**|資料類型之 creation 參數的描述。|  
|NULLABLE|**short**|指出資料行是否能包含 null 值。 它可能是下列其中一個值：<br /><br /> typeNoNulls (0)<br /><br /> typeNullable (1)<br /><br /> typeNullableUnknown (2)|  
|CASE_SENSITIVE|**boolean**|指出資料類型是否區分大小寫。 如果類型會區分大小寫則為 "**true**"，否則為 "**false**"。|  
|SEARCHABLE|**short**|指出資料行是否能用於 SQL WHERE 子句。 它可能是下列其中一個值：<br /><br /> typePredNone (0)<br /><br /> typePredChar (1)<br /><br /> typePredBasic (2)<br /><br /> typeSeachable (3)|  
|UNSIGNED_ATTRIBUTE|**boolean**|指出資料類型的正負號。 如果類型不帶正負號則為 "**true**"，否則為 "**false**"。|  
|FIXED_PREC_SCALE|**boolean**|指出資料類型可以是 money 值。 如果資料類型是 money 值則為"**true**"，否則為 "**false**"。|  
|AUTO_INCREMENT|**boolean**|指出資料類型可以自動遞增。 如果類型可以自動遞增則為 "**true**"，否則為 "**false**"。|  
|LOCAL_TYPE_NAME|**String**|資料類型的當地語系化名稱。|  
|MINIMUM_SCALE|**short**|小數點右邊的最大位數。|  
|MAXIMUM_SCALE|**short**|小數點右邊的最小位數。|  
|SQL_DATA_TYPE|**int**|JDBC 驅動程式不支援。|  
|SQL_DATETIME_SUB|**int**|JDBC 驅動程式不支援。|  
|NUM_PREC_RADIX|**int**|用來計算資料行可保留之最大數字的位元數目或位數。|  
|INTERVAL_PRECISION|**smallint**|間隔開頭有效位數的值。|  
|USERTYPE|**smallint**|**systypes** 資料表中的 **usertype** 值。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》。|  
  
> [!NOTE]  
>  如需 getTypeInfo 方法所回傳資料的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》中的＜sp_datatype_info (Transact-SQL)＞。  
  
## <a name="example"></a>範例  
 下列範例將示範如何使用 getTypeInfo 方法來傳回 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (或更新版本) 資料庫中所使用之資料類型的相關資訊。  
  
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
  
  
