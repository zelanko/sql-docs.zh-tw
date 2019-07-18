---
title: getIndexInfo 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getIndexInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a677cc6-8e33-4e57-8678-0849345aa8d0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 22414058b0763f32c2b991487e006b8de8e50611
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66774348"
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
  
 包含目錄名稱的 **String**。  
  
 *schema*  
  
 包含結構描述名稱的 **String**。  
  
 *table*  
  
 包含資料表名稱的 **String**。  
  
 *unique*  
  
 **true**如果只會傳回唯一值的索引。 **false**如果傳回的所有索引。  
  
 *approximate*  
  
 **true**如果結果會反映近似或過期的值。 **false**如果結果非常精確。  
  
## <a name="return-value"></a>傳回值  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getIndexInfo 方法是由 java.sql.DatabaseMetaData 介面中 getIndexInfo 方法指定。  
  
 透過 getIndexInfo 方法所傳回的結果將包含下列資訊：  
  
|[屬性]|類型|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|指定之資料表所在的資料庫名稱。|  
|TABLE_SCHEM|**String**|資料表的結構描述。|  
|TABLE_NAME|**String**|資料表的名稱。|  
|NON_UNIQUE|**boolean**|指出索引值是否可以不是唯一的。|  
|INDEX_QUALIFIER|**String**|索引擁有者的名稱。 當 TYPE 為 tableIndexStatistic 時，它會是 null。|  
|INDEX_NAME|**String**|索引的名稱。|  
|TYPE|**short**|索引的類型。 它可能是下列其中一個值：<br /><br /> tableIndexStatistic (0)<br /><br /> tableIndexClustered (1)<br /><br /> tableIndexHashed (2)<br /><br /> tableIndexOther (3)|  
|ORDINAL_POSITION|**short**|資料行在索引中的序數位置。 索引中的第一個資料行是 1。|  
|COLUMN_NAME|**String**|資料行的名稱。|  
|ASC_OR_DESC|**String**|用於索引定序的順序。 它可能是下列其中一個值：<br /><br /> A (遞增)<br /><br /> D (遞減)<br /><br /> NULL (不適用)<br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 一律會傳回 "A"。|  
|CARDINALITY|**int**|資料表中的資料列數，或索引中的唯一值數目。|  
|PAGES|**int**|用來儲存索引或資料表的頁數。|  
|FILTER_CONDITION|**String**|篩選條件。<br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 一律會傳回 null。|  
  
> [!NOTE]  
>  如需 getIndexInfo 方法所傳回資料的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》中的＜sp_indexes (Transact-SQL)＞。  
  
## <a name="example"></a>範例  
 下列範例會示範如何使用 getIndexInf 方法來傳回 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 範例資料庫中 Person.Contact 資料表索引和統計資料的相關資訊。  
  
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
  
  
