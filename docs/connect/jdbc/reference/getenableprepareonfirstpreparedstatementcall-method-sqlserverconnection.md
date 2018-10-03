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
manager: craigg
ms.openlocfilehash: 7e5a03b231b86be065ff19dd0f0a6818ba560bf5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47671736"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 傳回的值**enablePrepareOnFirstPreparedStatementCall**連接屬性。 如果為 false，第一次執行會呼叫 sp_executesql 並準備陳述式，當第二次的執行狀況就會呼叫 sp_prepexec，並實際設定備妥的陳述式控制代碼。 遵循執行，就會呼叫 sp_execute。 這減輕 sp_unprepare 備妥的陳述式需要關閉如果陳述式只執行一次。 呼叫 setDefaultEnablePrepareOnFirstPreparedStatementCall() 可以變更這個選項的預設值。

## <a name="syntax"></a>語法  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>傳回值
 A**布林**，其中包含的值**enablePrepareOnFirstPreparedStatementCall**連接屬性。

## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 這個方法是從 JDBC 驅動程式版本 6.4 可用且向外。
 
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
