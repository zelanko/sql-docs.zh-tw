---
title: getWorkstationID 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6a701de-a8fa-4668-9310-99a8c6e32c88
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98cde4953d60f13d1768b06dbfab9ada6ea8af55
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67978054"
---
# <a name="getworkstationid-method-sqlserverdatasource"></a>getWorkstationID 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回用來連接到資料來源之用戶端電腦的名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getWorkstationID()  
```  
  
## <a name="return-value"></a>傳回值  
 **String**，其中包含用戶端電腦名稱。  
  
## <a name="remarks"></a>備註  
 workstationID 是用戶端電腦或工作站的名稱。 如果未設定 workstationID 屬性，則會呼叫 InetAddress.getLocalHost().getHostName() 方法來建構預設值。 如果 getHostName 傳回空白值，則會呼叫 getHostAddress().toString() 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
