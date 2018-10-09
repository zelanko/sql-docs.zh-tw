---
title: setWorkstationID 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c1093615-90bf-4918-9f05-8abd765ffb03
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a29243c0b3b8922a2b6c743855080aa9e58abe87
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47771006"
---
# <a name="setworkstationid-method-sqlserverdatasource"></a>setWorkstationID 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定用來連接到資料來源之用戶端電腦的名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setWorkstationID(java.lang.String workstationID)  
```  
  
#### <a name="parameters"></a>參數  
 workstationID  
  
 ，包含用戶端電腦名稱。  
  
## <a name="remarks"></a>Remarks  
 workstationID 是用戶端電腦或工作站的名稱。 如果未設定 workstationID 屬性，預設值是藉由呼叫 InetAddress.getLocalHost().getHostName() 方法建構。 如果 getHostName 傳回空白值時，會呼叫 getHostAddress().toString() 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
