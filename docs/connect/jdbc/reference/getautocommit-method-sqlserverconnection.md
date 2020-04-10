---
title: getAutoCommit 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: af1f67f4-f568-4e58-abcc-5c809a89b547
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7d9e5545e0b7ed2953ba89b2351c09ae0fd3700a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920922"
---
# <a name="getautocommit-method-sqlserverconnection"></a>getAutoCommit 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件的目前自動認可模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean getAutoCommit()  
```  
  
## <a name="return-value"></a>傳回值  
 如果已啟用自動認可模式，則為 **true**，否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getAutoCommit 方法是由 java.sql.Connection 介面中的 getAutoCommit 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
