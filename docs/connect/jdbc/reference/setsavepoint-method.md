---
title: setSavepoint 方法 () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setSavepoint ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 11013055-4fd3-45a9-b2da-28b2908dad52
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c661df4fc5b60d52056c14bb9be1787a9a346fc0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924968"
---
# <a name="setsavepoint-method-"></a>setSavepoint 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在目前交易中建立未命名的儲存點，並傳回表示該儲存點的新 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Savepoint setSavepoint()  
```  
  
## <a name="return-value"></a>傳回值  
 SavePoint 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setSavePoint 方法是由 java.sql.Connection 介面中的 setSavePoint 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [setSavepoint 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
