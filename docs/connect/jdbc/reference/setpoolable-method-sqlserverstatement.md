---
title: setPoolable 方法 (SQLServerStatement) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f0f798c8-cafb-4acc-b85d-2e0059c91d92
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9647e2e2c887c95a647a4c5c6b3ca64efcf8c1d3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setpoolable-method-sqlserverstatement"></a>setPoolable 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  要求共用或不共用陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setPoolable(boolean poolable) throws SQLException  
```  
  
#### <a name="parameters"></a>參數  
 *可共用*  
  
 如果**true**，則表示應該共用陳述式。 如果**false**，則不應該共用陳述式。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 中指定的值*可共用*參數是提示，以指出應用程式是否想要共用陳述式的陳述式集區實作。 陳述式集區管理員會決定它是否使用該提示。  
  
 陳述式的集區值會套用到驅動程式所實作的內部陳述式快取，以及應用程式伺服器和其他應用程式所實作的外部陳述式快取。  
  
 根據預設，不是它建立 SQLServerStatement 物件。 SQLServerPreparedStatement 和 SQLServerCallableStatement 物件會建立可共用的。  
  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)如果已關閉的陳述式上呼叫這個方法會擲回。  
  
 [isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)傳回值，指出物件是否可共用。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
