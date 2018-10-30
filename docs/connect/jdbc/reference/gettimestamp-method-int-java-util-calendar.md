---
title: getTimestamp 方法 （int，java.util.Calendar） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTimestamp (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 161c559a-8651-44ba-a914-15eb6a612417
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc078598377ec7a866b90d68677cfd9302b6263a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673146"
---
# <a name="gettimestamp-method-int-javautilcalendar"></a>getTimestamp 方法 (int, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式語言，並配合所指定參數索引和日曆物件來擷取指定的參數值當作 java.sql.Timestamp 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Timestamp getTimestamp(int index,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 指出參數索引的 **int**。  
  
 *cal*  
  
 月曆物件。  
  
## <a name="return-value"></a>傳回值  
 時間戳記物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getTimestamp 方法是由 java.sql.CallableStatement 介面中的 getTimestamp 方法指定。  
  
 這個方法只會傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime** 和 **smalldatetime** 資料行中的值。  
  
## <a name="see-also"></a>另請參閱  
 [getTimestamp 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
