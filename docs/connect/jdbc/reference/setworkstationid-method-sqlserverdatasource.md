---
title: setWorkstationID 方法 (SQLServerDataSource) | Microsoft Docs
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
ms.openlocfilehash: 08b09958276a5cc7f7cc3de6e56f7d7336ca9e64
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67972029"
---
# <a name="setworkstationid-method-sqlserverdatasource"></a>setWorkstationID 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定用來連接到資料來源之用戶端電腦的名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setWorkstationID(java.lang.String workstationID)  
```  
  
#### <a name="parameters"></a>參數  
 *workstationID*  
  
 **String**，其中包含用戶端電腦名稱。  
  
## <a name="remarks"></a>備註  
 workstationID 是用戶端電腦或工作站的名稱。 如果未設定 workstationID 屬性，則會呼叫 InetAddress.getLocalHost().getHostName() 方法來建構預設值。 如果 getHostName 傳回空白值，則會呼叫 getHostAddress().toString() 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
