---
title: close 方法 (SQLServerResultSet) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8f3adf5b-874e-4cf2-b4ef-672dda42d77a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: deea90b13bb4bb99c504f5eaa344babdf4a1c680
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32830733"
---
# <a name="close-method-sqlserverresultset"></a>close 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  釋放這個[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件的資料庫和 JDBC 資源，立即而不是等待這種情形時自動關閉。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此 close 方法是由 java.sql.ResultSet 介面中之關閉方法指定。  
  
 SQLServerResultSet 物件會自動關閉[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)它的 SQLServerStatement 物件時，已關閉、 重新執行，或用來擷取下一個結果，從順序產生的多個結果的物件. 當記憶體回收，就也會自動關閉 SQLServerResultSet 物件。  
  
 當執行會產生單一大型順向、唯讀結果集的陳述式時，您可能只會對所傳回結果集中的部分開頭資料列集有興趣。 在此情況下，應用程式可能會呼叫[取消](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)相關的陳述式物件，再關閉該結果的方法設定以捨棄剩餘不必要的資料列所需的處理時間降至最低。 我們建議您在決定是否使用這項技巧時，權衡取捨可以節省的處理時間，以及伺服器在取消該執行時所需要的時間和額外往返。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
