---
title: "acceptsURL 方法 (SQLServerDriver) |Microsoft 文件"
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
- SQLServerDriver.acceptsURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fc744566-7191-4b15-9f76-b4b8087fb14a
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f45fb8e673528719750e18af08ccadcebf4d084c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="acceptsurl-method-sqlserverdriver"></a>acceptsURL 方法 (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  檢查給定的 URL 是否有效。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean acceptsURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>參數  
 *url*  
  
 A**字串**包含 URL 的值用來連接到資料庫。  
  
## <a name="return-value"></a>傳回值  
 **true**給定的 URL 是否有效。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 acceptsURL 方法是由 java.sql.Driver 介面中 acceptsURL 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDriver 方法](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver 成員](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver 類別](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
