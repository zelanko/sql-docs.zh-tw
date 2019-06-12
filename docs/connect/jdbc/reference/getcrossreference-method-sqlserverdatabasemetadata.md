---
title: getCrossReference 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCrossReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 099dd0bf-b017-479d-9696-f5b06f4c6bf9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2fc70ed3e449840793dbd32e4d2014031256f3bd
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66763007"
---
# <a name="getcrossreference-method-sqlserverdatabasemetadata"></a>getCrossReference 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取給定外部索引鍵資料表中之外部索引鍵資料行的描述，該資料表會參考給定主索引鍵資料表的主索引鍵資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getCrossReference(java.lang.String cat1,  
                                            java.lang.String schem1,  
                                            java.lang.String tab1,  
                                            java.lang.String cat2,  
                                            java.lang.String schem2,  
                                            java.lang.String tab2)  
```  
  
#### <a name="parameters"></a>參數  
 *cat1*  
  
 **String**，其中包含資料表的目錄名稱，而此資料表含有主索引鍵。  
  
 *schem1*  
  
 **String**，其中包含資料表的結構描述名稱，而此資料表含有主索引鍵。  
  
 *tab1*  
  
 **String**，其中包含資料表的資料表名稱，而此資料表含有主索引鍵。  
  
 *cat2*  
  
 **String**，其中包含資料表的目錄名稱，而此資料表含有外部索引鍵。  
  
 *schem2*  
  
 **String**，其中包含資料表的結構描述名稱，而此資料表含有外部索引鍵。  
  
 *tab2*  
  
 **String**，其中包含資料表的資料表名稱，而此資料表含有外部索引鍵。  
  
## <a name="return-value"></a>傳回值  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getCrossReference 方法是由 java.sql.DatabaseMetaData 介面中 getCrossReference 方法指定。  
  
 透過 getCrossReference 方法所傳回的結果將包含下列資訊：  
  
|[屬性]|類型|Description|  
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
>  如需 getCrossReference 方法所傳回資料的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》中的＜sp_fkeys (Transact-SQL)＞。  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 getCrossReference 方法來傳回有關 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 範例資料庫中 Person.Contact 與 HumanResources.Employee 資料表之間主索引鍵和外部索引鍵關聯性的資訊。  
  
```  
public static void executeGetCrossReference(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getCrossReference("AdventureWorks", "Person", "Contact", null, "HumanResources", "Employee");  
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
  
  
