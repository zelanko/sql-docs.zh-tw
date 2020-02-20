---
title: getSchemas 方法 () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSchemas
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: adba0ee6-ff6d-4215-b646-62c735be3fe9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0a5f453e6300258cacffa6606259f85cdd25977
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67980086"
---
# <a name="getschemas-method-"></a>getSchemas 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前資料庫中所提供的結構描述名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getSchemas()  
```  
  
## <a name="return-value"></a>傳回值  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getSchemas 方法是由 java.sql.DatabaseMetaData 介面中的 getSchemas 方法指定。  
  
 透過 getSchemas 方法所傳回的結果集將包含下列資訊：  
  
|名稱|類型|描述|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**String**|結構描述的名稱。|  
|TABLE_CATALOG|**String**|結構描述的目錄名稱。|  
  
 這些結果會依據 TABLE_CATALOG 排列，接著再依據 TABLE_SCHEM 排列。 每個資料列都是以 TABLE_SCHEM 做為第一個資料列，以 TABLE_CATALOG 做為第二個資料列。  
  
> [!NOTE]  
>  如需 getSchemas 方法所傳回資料的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》中的＜sys.schemas (Transact-SQL)＞。  
  
## <a name="example"></a>範例  
 下列範例會示範當連接引數指定要使用的資料庫時，如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中使用 getSchemas 方法來傳回目錄及其相關聯結構描述名稱的相關資訊。  
  
```  
public static void executeGetSchemas(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getSchemas();  
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
  
  
