---
title: "getCrossReference 方法 (SQLServerDatabaseMetaData) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getCrossReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 099dd0bf-b017-479d-9696-f5b06f4c6bf9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 70da15793b0a6f5e8687756404a45a23fd805161
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

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
  
 A**字串**，其中包含之資料表的主索引鍵的目錄名稱。  
  
 *schem1*  
  
 A**字串**包含主索引鍵資料表的結構描述名稱。  
  
 *tab1*  
  
 A**字串**，其中包含之資料表的主索引鍵資料表名稱。  
  
 *cat2*  
  
 A**字串**，其中包含之資料表的外部索引鍵的目錄名稱。  
  
 *schem2*  
  
 A**字串**，其中包含外部索引鍵資料表的結構描述名稱。  
  
 *tab2*  
  
 A**字串**，其中包含之資料表的外部索引鍵資料表名稱。  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getCrossReference 方法是由 java.sql.DatabaseMetaData 介面中 getCrossReference 方法指定。  
  
 GetCrossReference 方法所傳回的結果集將包含下列資訊：  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|PKTABLE_CAT|**字串**|包含主索引鍵資料表的目錄名稱。|  
|PKTABLE_SCHEM|**字串**|主索引鍵資料表的結構描述名稱。|  
|PKTABLE_NAME|**字串**|主索引鍵資料表的名稱。|  
|PKCOLUMN_NAME|**字串**|主索引鍵的資料行名稱。|  
|FKTABLE_CAT|**字串**|包含外部索引鍵資料表的目錄名稱。|  
|FKTABLE_SCHEM|**字串**|外部索引鍵資料表的結構描述名稱。|  
|FKTABLE_NAME|**字串**|外部索引鍵資料表的名稱。|  
|FKCOLUMN_NAME|**字串**|外部索引鍵的資料行名稱。|  
|KEY_SEQ|**短**|資料行在多重資料行主索引鍵中的序號。|  
|UPDATE_RULE|**短**|當 SQL 作業為更新時套用到外部索引鍵的動作。 它可能是下列其中一個值：<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|DELETE_RULE|**短**|當 SQL 作業為刪除時套用到外部索引鍵的動作。 它可能是下列其中一個值：<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|FK_NAME|**字串**|外部索引鍵的名稱。|  
|PK_NAME|**字串**|主索引鍵的名稱。|  
|DEFERRABILITY|**短**|指出外部索引鍵條件約束的評估是否可以延遲到認可之前。 它可能是下列其中一個值：<br /><br /> importedKeyInitiallyDeferred (5)<br /><br /> importedKeyInitiallyImmediate (6)<br /><br /> importedKeyNotDeferrable (7)|  
  
> [!NOTE]  
>  多個 getCrossReference 方法所傳回的資料的詳細資訊，請參閱 「 sp_fkeys (TRANSACT-SQL) 」，在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 getCrossReference 方法來傳回中 Person.Contact 與 HumanResources.Employee 資料表之間的主要和外部索引鍵關聯性的相關資訊[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫。  
  
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
  
  

