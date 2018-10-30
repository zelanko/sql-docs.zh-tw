---
title: setQueryTimeout 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setQueryTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0c513265-cd0c-4b38-9494-94458c17a16d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09c984b0d4a0bfa1fedb57f60532a721b16afccf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47621397"
---
# <a name="setquerytimeout-method-sqlserverstatement"></a>setQueryTimeout 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定驅動程式將等候這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件執行指定秒數的秒數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setQueryTimeout(int seconds)  
```  
  
#### <a name="parameters"></a>參數  
 *seconds*  
  
 **int**，指出等候的秒數，如果沒有任何限制則為 0。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 setQueryTimeout 方法是由 java.sql.Statement 介面中的 setQueryTimeout 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
