---
title: setReadOnly 方法 (SQLServerConnection) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.setReadOnly
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bd11fd50-f092-43a0-a6bc-c63e70cff8da
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b94f1b5555fd0bb90afaf492ab2ab61a643372bb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setreadonly-method-sqlserverconnection"></a>setReadOnly 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  切換這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件成為唯讀模式，當作 JDBC 驅動程式啟用資料庫最佳化的提示。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 不支援這個方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setReadOnly(boolean readOnly)  
```  
  
#### <a name="parameters"></a>參數  
 *readOnly*  
  
 如果連線應處於唯讀模式則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 SetReadOnly 方法 java.sql.Connection 介面中所指定此 setReadOnly 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
