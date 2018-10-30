---
title: cancel 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.cancel
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 276bd9c1-9329-4fc9-9622-ed673c83a12d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49bd0845e6bebf1365ab8c26cb48bda2a92a6b4e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840166"
---
# <a name="cancel-method-sqlserverstatement"></a>cancel 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  取消目前正由這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件執行的 SQL 陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void cancel()  
```  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個取消方法是由 java.sql.Statement 介面中的取消方法指定。  
  
 當執行會產生單一大型順向、唯讀結果集的陳述式時，您可能只會對所傳回結果集中的部分開頭資料列集有興趣。 在這種情況下，應用程式可能會先呼叫相關聯陳述式物件的 [cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md) 方法，再關閉該結果集，以便盡量縮短捨棄剩餘不必要資料列時所需要的處理時間。 我們建議您在決定是否使用這項技巧時，權衡取捨可以節省的處理時間，以及伺服器在取消該執行時所需要的時間和額外往返。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
