---
title: isClosed 方法 (SQLServerConnection) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 776c719a01378a30198b7a3bcc4134478ebeb742
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928672"
---
# <a name="isclosed-method-sqlserverconnection"></a>isClosed 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件是否已關閉。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>傳回值  
 連線已關閉時為 **true**，否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 isClosed 方法是由 java.sql.Connection 介面中的 isClosed 方法指定。  
  
 驗證已呼叫之 SQLServerConnection 物件的狀態。 如果已經在連接上呼叫 [close](../../../connect/jdbc/reference/close-method-sqlserverconnection.md) 方法或是發生了某些嚴重錯誤，連接就會關閉。 這個方法只有在呼叫 close 方法之後呼叫時，才會傳回 **true**。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
