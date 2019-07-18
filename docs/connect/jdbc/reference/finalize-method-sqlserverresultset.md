---
title: finalize 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.finalize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49bc879d-822b-42da-bc20-2394865f1f0f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 854da2b16cf680ac6ce54ae44a4bf1296cdbfd2c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796859"
---
# <a name="finalize-method-sqlserverresultset"></a>finalize 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  明確地關閉這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void finalize()  
```  
  
## <a name="remarks"></a>Remarks  
 如果應用程式不會關閉結果集，則關閉結果集。 這個方法存在的目的只是為了符合 JDBC 規格。 因為 Java Virtual Machine (JVM) 不保證何時有機會執行 finalizer，所以不願意明確關閉其結果集的應用程式仍然有可能在使用相同連接的另一個陳述式上發生死結，而且在一般伺服器資源上遭到封鎖 (如資料列鎖定)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
