---
title: close 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8f3adf5b-874e-4cf2-b4ef-672dda42d77a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e78dbb981938e9af2fbe894919368da17347941a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955581"
---
# <a name="close-method-sqlserverresultset"></a>close 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  立刻釋放這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的資料庫和 JDBC 資源，而不等待當其自動關閉時才進行釋放。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 close 方法是由 java.sql.ResultSet 介面中的 close 方法指定。  
  
 當 SQLServerStatement 物件遭到關閉、重新執行，或用來從一連串多個結果中擷取下一個結果時，產生 SQLServerResultSet 物件的 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件會自動關閉該結果集物件。 SQLServerResultSet 物件也會在進行記憶體回收時自動關閉。  
  
 當執行會產生單一大型順向、唯讀結果集的陳述式時，您可能只會對所傳回結果集中的部分開頭資料列集有興趣。 在這種情況下，應用程式可能會先呼叫相關聯陳述式物件的 [cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md) 方法，再關閉該結果集，以便盡量縮短捨棄剩餘不必要資料列時所需要的處理時間。 我們建議您在決定是否使用這項技巧時，權衡取捨可以節省的處理時間，以及伺服器在取消該執行時所需要的時間和額外往返。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
