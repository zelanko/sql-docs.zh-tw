---
title: "setDisableStatementPooling 方法 (SQLServerConnection) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2018
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
- SQLServerConnection.setDisableStatementPooling
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3bb7b1d2810bd29183d6c3182f8a2035271e615
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2018
---
# <a name="setdisablestatementpooling-method-sqlserverconnection"></a>setDisableStatementPooling 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 設定為 true 或 false 的陳述式集區。 如果為 false，可讓共用以用於結合，以 statementPoolingCacheSize 值 > 0 的陳述式。

## <a name="syntax"></a>語法  
  
```  
  
public void setDisableStatementPooling(boolean disableStatementPooling)  
```  

#### <a name="parameters"></a>參數  
 *disableStatementPooling*  
  
 新值**disableStatementPooling**連接屬性。  
 
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>備註  
 這個方法是從 JDBC 驅動程式版本 6.4 可用且向外。
 
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
