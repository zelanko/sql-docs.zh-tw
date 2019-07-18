---
title: isReadOnly 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.isReadOnly
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 902fd2c1-05e0-436e-9779-c048cdb8475a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2faac8d83f79c60551c0d62f18e64ccd427f91bc
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796374"
---
# <a name="isreadonly-method-sqlserverconnection"></a>isReadOnly 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件是否處於唯讀模式。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 目前不支援這個方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isReadOnly()  
```  
  
## <a name="return-value"></a>傳回值  
 如果連接處於唯讀模式，則為 **true**；如果不是，則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 isReadOnly 方法是由 java.sql.Connection 介面中的 isReadOnly 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
