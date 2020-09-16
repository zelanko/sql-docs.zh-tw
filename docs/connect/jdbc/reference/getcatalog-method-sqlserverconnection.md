---
description: getCatalog 方法 (SQLServerConnection)
title: getCatalog 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e87ef65f-4b5a-4e1c-8db5-7f0932390bb0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc4b720ccf920d1f9fe97ed29f2a2a237e24939e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436880"
---
# <a name="getcatalog-method-sqlserverconnection"></a>getCatalog 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件的目前目錄名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getCatalog()  
```  
  
## <a name="return-value"></a>傳回值  
 包含目錄名稱的 **String**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此 getCatalog 方法是由 java.sql.Connection 介面中的 getCatalog 方法所指定。  
  
 傳回 SQLServerConnection 物件的目前目錄屬性，如果未設定則傳回 Null。 此目錄屬性會使用 [setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md) 方法來明確設定，或者藉由讀取 TDS 上目前目錄的環境變更來以隱含方式更新。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
