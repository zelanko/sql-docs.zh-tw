---
title: "rowDeleted 方法 (SQLServerResultSet) |Microsoft 文件"
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
- SQLServerResultSet.rowDeleted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9c6db315-e614-4604-b020-41af6a214cc1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f2c4e8e106f749fd087cf47d2c444743ef27172
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="rowdeleted-method-sqlserverresultset"></a>rowDeleted 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出資料列是否已遭刪除。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean rowDeleted()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果一個資料列已經刪除而且偵測到刪除則。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 rowDeleted 方法是由 java.sql.ResultSet 介面中的 rowDeleted 方法來指定。  
  
 刪除的資料列可能會在結果集中留下可見的漏洞。 這個方法可用來偵測結果集中的漏洞。 傳回的值取決於是否這[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件可以偵測到刪除。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]會偵測所有可更新的資料指標類型，已刪除的資料列，雖然偵測作業屬於暫時順向和動態資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
