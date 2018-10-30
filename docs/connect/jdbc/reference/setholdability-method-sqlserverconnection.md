---
title: setHoldability 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 552eebd0-4c38-43f0-961f-35244f99109b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37181dfc2a2fa7b3e166d00e83130c2758e28533
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47638640"
---
# <a name="setholdability-method-sqlserverconnection"></a>setHoldability 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的保留性變更為指定的保留性，這些物件是使用此 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 物件所建立。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setHoldability(int nNewHold)  
```  
  
#### <a name="parameters"></a>參數  
 *nNewHold*  
  
 **int** 值，包含下列其中一個保留性等級：  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 setHoldability 方法是由 java.sql.Connection 介面中的 setHoldability 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
