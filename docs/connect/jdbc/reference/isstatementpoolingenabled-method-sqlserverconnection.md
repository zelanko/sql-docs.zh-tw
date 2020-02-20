---
title: isStatementPoolingEnabled 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.isStatementPoolingEnabled
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d2f5178c8a2ce5b527ce70e6a3d8fc139ccc9c72
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67977207"
---
# <a name="isstatementpoolingenabled-method-sqlserverconnection"></a>isStatementPoolingEnabled 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 傳回陳述式共用是否已針對此連線啟用。

## <a name="syntax"></a>語法  
  
```  
  
public boolean isStatementPoolingEnabled()  
```  

## <a name="return-value"></a>傳回值
 包含指出陳述式共用是否已啟用之旗標的**布林值**。

## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>備註  
 從 JDBC 驅動程式 6.4 版開始，可以使用此方法。
 
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
