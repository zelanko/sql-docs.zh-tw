---
title: setReadOnly 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setReadOnly
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bd11fd50-f092-43a0-a6bc-c63e70cff8da
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c3f73a9fc5a6876bd0490fef73624664f84a0885
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799595"
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
  
## <a name="remarks"></a>Remarks  
 這個 setReadOnly 方法是由 java.sql.Connection 介面中的 setReadOnly 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
