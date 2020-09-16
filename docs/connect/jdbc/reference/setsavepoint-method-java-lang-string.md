---
description: setSavepoint 方法 (java.lang.String)
title: setSavepoint 方法 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setSavepoint (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1cf15ec4-d9d9-4ab3-bfee-2ea43ff609a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 57ed08c322b8579b92165306397fb26312d95fa3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458406"
---
# <a name="setsavepoint-method-javalangstring"></a>setSavepoint 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定名稱，在目前交易中建立儲存點，並傳回表示該儲存點的新 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Savepoint setSavepoint(java.lang.String sName)  
```  
  
#### <a name="parameters"></a>參數  
 *sName*  
  
 **String** 值，其中包含此儲存點的名稱。  
  
## <a name="return-value"></a>傳回值  
 SavePoint 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此 setSavePoint 方法是由 java.sql.Connection 介面中的 setSavePoint 方法所指定。  
  
 *sName* 引數會由 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 自動逸出。  
  
## <a name="see-also"></a>另請參閱  
 [setSavepoint 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
