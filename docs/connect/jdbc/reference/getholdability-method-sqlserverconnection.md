---
title: getHoldability 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b1644791-c36a-4837-86c4-9299537ee1c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3df60cd50c56a194c7939a30cf2a75a21c2a845
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921518"
---
# <a name="getholdability-method-sqlserverconnection"></a>getHoldability 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的目前保留性，這些物件是使用此 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件所建立。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>傳回值  
 **int** 值，包含下列其中一個保留性等級：  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getHoldability 方法是由 java.sql.Connection 介面中的 getHoldability 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
