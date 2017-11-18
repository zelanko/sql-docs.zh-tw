---
title: "connect 方法 (SQLServerDriver) |Microsoft 文件"
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
- SQLServerDriver.connect
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 43813a4c-1cc7-4659-ba27-f1786f1371eb
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 07b4331ee938c2eb8b86a263e0fb4bd6f17a241f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="connect-method-sqlserverdriver"></a>connect 方法 (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立與資料庫的連接。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Connection connect(java.lang.String Url,  
                                   java.util.Properties suppliedProperties)  
```  
  
#### <a name="parameters"></a>參數  
 *Url*  
  
 A**字串**值，其中包含用來連接到資料庫的 URL。  
  
 *suppliedProperties*  
  
 當做連接引數使用的一組字串值。  
  
## <a name="return-value"></a>傳回值  
 連接物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個連接的方法是由 java.sql.Driver 介面中的 connect 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDriver 方法](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver 成員](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver 類別](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  

