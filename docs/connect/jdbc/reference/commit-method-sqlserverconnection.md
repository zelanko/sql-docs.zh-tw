---
title: commit 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c7346165-51bf-4844-b64c-29833c147236
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: dafb8b3c5016d0be191e06eefb5b5ca80b9ec0de
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66777387"
---
# <a name="commit-method-sqlserverconnection"></a>commit 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使從上一次認可或回復後的所有變更成為永久狀態，並且釋放目前由這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件保留的任何資料庫鎖定。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void commit()  
```  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 commit 方法是由 java.sql.Connection 介面中的 commit 方法指定。  
  
 只有當已經停用自動認可模式時，才應該使用這個方法。  
  
 請注意，如果用戶端開始手動交易，然後 SQL Server 基於某個原因回復此手動交易，這個方法將會失敗並擲回例外狀況。 例如，如果用戶端呼叫的預存程序會明確呼叫 ROLLBACK TRANSACTION，然後用戶端呼叫 commit 方法，則會擲回例外狀況。 此外，如果 SQL Server 引發相當嚴重的錯誤 (16 或更高嚴重性等級) 來回復用戶端起始的手動交易，則後續的 commit 方法呼叫會擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
