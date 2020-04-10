---
title: getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerConnection) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 203ed2f6a68e11af8c63157a850a146ea8d81464
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80909580"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 傳回 **enablePrepareOnFirstPreparedStatementCall** 連接屬性的值。 如果為 false，則第一次執行將會呼叫 sp_executesql 而不是備妥陳述式，一旦第二次執行時，就會呼叫 sp_prepexec 並實際設定備妥陳述式控制代碼。 下列執行將會呼叫 sp_execute。 如果該陳述式僅執行一次，則無需在備妥陳述式結束時使用 sp_unprepare。 您可以藉由呼叫 setDefaultEnablePrepareOnFirstPreparedStatementCall() 來變更這個選項的預設值。

## <a name="syntax"></a>語法  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>傳回值
 **布林值**，其中包含 **enablePrepareOnFirstPreparedStatementCall** 連接屬性的值。

## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>備註  
 從 JDBC 驅動程式 6.4 版開始，可以使用此方法。
 
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
