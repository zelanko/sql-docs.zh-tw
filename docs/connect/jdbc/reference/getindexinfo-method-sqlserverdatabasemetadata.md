---
title: "getIndexInfo 方法 (SQLServerDatabaseMetaData) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getIndexInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a677cc6-8e33-4e57-8678-0849345aa8d0
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 028937d023b6cf899eb5fa47354cb0c5d21545bc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getindexinfo-method-sqlserverdatabasemetadata"></a>getIndexInfo 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取給定資料表中的索引和統計資料的描述。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getIndexInfo(java.lang.String cat,  
                                       java.lang.String schema,  
                                       java.lang.String table,  
                                       boolean unique,  
                                       boolean approximate)  
```  
  
#### <a name="parameters"></a>參數  
 *cat*  
  
 A**字串**，其中包含目錄名稱。  
  
 *結構描述*  
  
 A**字串**，其中包含結構描述名稱。  
  
 *table*  
  
 A**字串**，其中包含資料表名稱。  
  
 *唯一*  
  
 **true**是否只會傳回唯一值的索引。 **false**如果傳回所有索引。  
  
 *近似*  
  
 **true**如果結果會反映近似或過期的值。 **false**如果結果非常精確。  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getIndexInfo 方法是由 java.sql.DatabaseMetaData 介面中 getIndexInfo 方法指定。  
  
 GetIndexInfo 方法所傳回的結果集將包含下列資訊：  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**字串**|指定之資料表所在的資料庫名稱。|  
|TABLE_SCHEM|**字串**|資料表的結構描述。|  
|TABLE_NAME|**字串**|資料表的名稱。|  
|NON_UNIQUE|**boolean**|指出索引值是否可以不是唯一的。|  
|INDEX_QUALIFIER|**字串**|索引擁有者的名稱。 當 TYPE 為 tableIndexStatistic 時，它會是 null。|  
|INDEX_NAME|**字串**|索引的名稱。|  
|TYPE|**短**|索引的類型。 它可能是下列其中一個值：<br /><br /> tableIndexStatistic (0)<br /><br /> tableIndexClustered (1)<br /><br /> tableIndexHashed (2)<br /><br /> tableIndexOther (3)|  
|ORDINAL_POSITION|**短**|資料行在索引中的序數位置。 索引中的第一個資料行是 1。|  
|COLUMN_NAME|**字串**|資料行的名稱。|  
|ASC_OR_DESC|**字串**|用於索引定序的順序。 它可能是下列其中一個值：<br /><br /> A (遞增)<br /><br /> D (遞減)<br /><br /> NULL (不適用)<br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]一律會傳回"A"。  |  
|CARDINALITY|**int**|資料表中的資料列數，或索引中的唯一值數目。|  
|PAGES|**int**|用來儲存索引或資料表的頁數。|  
|FILTER_CONDITION|**字串**|篩選條件。<br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]一定會傳回 null。  |  
  
> [!NOTE]  
>  多個 getIndexInfo 方法所傳回的資料的詳細資訊，請參閱 「 < sp_indexes (TRANSACT-SQL) 」，在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 getIndexInfo 方法來傳回資訊的索引和統計資料中的 Person.Contact 資料表[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫。  
  
```  
public static void executeGetIndexInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getIndexInfo("AdventureWorks", "Person", "Contact", false, true);  
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
  
  

