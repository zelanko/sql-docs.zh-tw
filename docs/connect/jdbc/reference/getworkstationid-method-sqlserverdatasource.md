---
title: getWorkstationID 方法 (SQLServerDataSource) |Microsoft 文件
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
- SQLServerDataSource.getWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6a701de-a8fa-4668-9310-99a8c6e32c88
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4466d3bfe0a088f4694eb01bef74e8ac34c4f8b2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32838763"
---
# <a name="getworkstationid-method-sqlserverdatasource"></a>getWorkstationID 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回用來連接到資料來源之用戶端電腦的名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getWorkstationID()  
```  
  
## <a name="return-value"></a>傳回值  
 A**字串**，其中包含用戶端電腦名稱。  
  
## <a name="remarks"></a>備註  
 workstationID 是用戶端電腦或工作站的名稱。 如果未設定 workstationID 屬性，預設值是藉由呼叫 InetAddress.getLocalHost().getHostName() 方法建構。 如果 getHostName 傳回空白值時，會呼叫 getHostAddress().toString() 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
