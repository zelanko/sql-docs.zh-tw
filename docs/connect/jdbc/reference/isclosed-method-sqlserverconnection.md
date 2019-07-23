---
title: isClosed 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.isClosed
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3560ab18-4350-4d02-9716-439f0c2f7142
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45e56a0a5ddb7cf8aece6813d421b7ebb1685408
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977713"
---
# <a name="isclosed-method-sqlserverconnection"></a>isClosed 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件是否已關閉。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>傳回值  
 如果連接已關閉,**則為 true** , 否則為**false** 。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 isClosed 方法是由連接介面中的 isClosed 方法指定。  
  
 驗證所呼叫 SQLServerConnection 物件的狀態。 如果已經在連接上呼叫 [close](../../../connect/jdbc/reference/close-method-sqlserverconnection.md) 方法或是發生了某些嚴重錯誤，連接就會關閉。 這個方法只有在呼叫 close 方法之後呼叫時，才會傳回 **true**。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
