---
title: "setNString 方法 （int，java.lang.String） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b7da6d44-f5b1-44f8-95f5-40179968b1b0
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b84ef0d56dfb73670571020e911b200afaac1db
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="setnstring-method-int-javalangstring"></a>setNString 方法 (int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定的參數設定為指定**字串**物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setNString(int parameterIndex,  
                                                  java.lang.String value)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterIndex*  
  
 **Int** ，指出參數索引。  
  
 *value*  
  
 A**字串**物件，其中包含參數值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個方法應用於**NCHAR**， **NVARCHAR**， **NTEXT**，和**XML**資料型別。  
  
 SetNString 方法 java.sql.PreparedStatement 介面中所指定此 setNString 方法。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
