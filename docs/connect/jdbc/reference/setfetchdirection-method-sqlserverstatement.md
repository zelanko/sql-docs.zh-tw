---
title: "setFetchDirection 方法 (SQLServerStatement) |Microsoft 文件"
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
- SQLServerStatement.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 18176517-2fb3-4266-924d-0f01253083d2
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 510736faf5189cf596c96809f6601fb38e50977d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setfetchdirection-method-sqlserverstatement"></a>setFetchDirection 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  提供[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]提示，當做應能處理結果集資料列的方向。  
  
> [!NOTE]  
>  JDBC Driver 目前會忽略由這個方法所給定的提示。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setFetchDirection(int nDir)  
```  
  
#### <a name="parameters"></a>參數  
 *nDir*  
  
 **Int** ，指出資料列處理方向，它可以是下列值之一：  
  
 FETCH_FORWARD  
  
 FETCH_REVERSE  
  
 FETCH_UNKNOWN  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setFetchDirection 方法是由 java.sql.Statement 介面中的 setFetchDirection 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

