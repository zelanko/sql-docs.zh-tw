---
title: getImportedKeys 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getImportedKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc8c1a5e-700e-4059-a5ed-5013bbb87fb6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2418bd5e62f00e46ddc329c1c7ba987505fb5a7f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982822"
---
# <a name="getimportedkeys-method-sqlserverdatabasemetadata"></a>getImportedKeys 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取主索引鍵資料行的描述，這些資料行會由資料表中的外部索引鍵資料行所參考。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getImportedKeys(java.lang.String cat,  
                                          java.lang.String schema,  
                                          java.lang.String table)  
```  
  
#### <a name="parameters"></a>參數  
 *cat*  
  
 包含目錄名稱的 **String**。  
  
 *schema*  
  
 包含結構描述名稱的 **String**。  
  
 *table*  
  
 包含資料表名稱的 **String**。  
  
## <a name="return-value"></a>傳回值  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getImportedKeys 方法是由 java.sql.DatabaseMetaData 介面中的 getImportedKeys 方法指定。  
  
 透過 getImportedKeys 方法所傳回的結果將包含下列資訊：  
  
|名稱|類型|描述|  
|----------|----------|-----------------|  
|PKTABLE_CAT|**String**|包含主索引鍵資料表的目錄名稱。|  
|PKTABLE_SCHEM|**String**|主索引鍵資料表的結構描述名稱。|  
|PKTABLE_NAME|**String**|主索引鍵資料表的名稱。|  
|PKCOLUMN_NAME|**String**|主索引鍵的資料行名稱。|  
|FKTABLE_CAT|**String**|包含外部索引鍵資料表的目錄名稱。|  
|FKTABLE_SCHEM|**String**|外部索引鍵資料表的結構描述名稱。|  
|FKTABLE_NAME|**String**|外部索引鍵資料表的名稱。|  
|FKCOLUMN_NAME|**String**|外部索引鍵的資料行名稱。|  
|KEY_SEQ|**short**|資料行在多重資料行主索引鍵中的序號。|  
|UPDATE_RULE|**short**|當 SQL 作業為更新時套用到外部索引鍵的動作。 它可能是下列其中一個值：<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|DELETE_RULE|**short**|當 SQL 作業為刪除時套用到外部索引鍵的動作。 它可能是下列其中一個值：<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|FK_NAME|**String**|外部索引鍵的名稱。|  
|PK_NAME|**String**|主索引鍵的名稱。|  
|DEFERRABILITY|**short**|指出外部索引鍵條件約束的評估是否可以延遲到認可之前。 它可能是下列其中一個值：<br /><br /> importedKeyInitiallyDeferred (5)<br /><br /> importedKeyInitiallyImmediate (6)<br /><br /> importedKeyNotDeferrable (7)|  
  
> [!NOTE]  
>  如需 getImportedKeys 方法所傳回資料的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》中的＜sp_fkeys (Transact-SQL)＞。  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 getImportedKeys 方法來傳回所有主索引鍵的相關資訊，而這些主索引鍵會在 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 範例資料庫中參考 Person.Address 資料表的外部索引鍵。  
  
```  
public static void executeGetImportedKeys(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getImportedKeys("AdventureWorks", "Person", "Address");  
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
  
  
