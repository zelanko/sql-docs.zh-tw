---
title: getResultSetHoldability 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getResultSetHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 053549ee-2018-47ab-9538-789dac2b150a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3fda68e39b09a21bfc9ac0caea3ce475e5cd8d71
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643971"
---
# <a name="getresultsetholdability-method-sqlserverstatement"></a>getResultSetHoldability 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取由這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件產生的 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件結果集保留性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final int getResultSetHoldability()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出結果集的保留性。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getResultSetHoldability 方法是由 java.sql.Statement 介面中的 getResultSetHoldability 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
