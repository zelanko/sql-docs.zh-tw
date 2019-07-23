---
title: getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac1cf4dbd8c8c14b5c97dbfecbe81d397c1598ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983441"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 傳回**enablePrepareOnFirstPreparedStatementCall**連接屬性的值。 如果為 false, 第一次執行會呼叫 sp_executesql, 而不是準備語句, 則在第二次執行時, 它會呼叫 sp_prepexec, 並實際設定備妥的語句控制碼。 下列執行會呼叫 sp_execute。 如此一來, 如果語句只執行一次, 就能減輕備妥的語句關閉 sp_unprepare 的需求。 您可以藉由呼叫 setDefaultEnablePrepareOnFirstPreparedStatementCall () 來變更這個選項的預設值。

## <a name="syntax"></a>語法  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>傳回值
 包含**enablePrepareOnFirstPreparedStatementCall**連接屬性值的**布林**值。

## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 這個方法可從 JDBC 驅動程式6.4 版和之後版本取得。
 
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
