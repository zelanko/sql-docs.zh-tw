---
title: setFailoverPartner 方法 (SQLServerDataSource) |Microsoft 文件
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
- SQLServerDataSource.setFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5310b7c2-9d10-474f-ad3a-218fe5da694b
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6e08b2189e2eca12a44802ded59775b63a0fcb6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setfailoverpartner-method-sqlserverdatasource"></a>setFailoverPartner 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定用於資料庫鏡像組態的容錯移轉伺服器名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setFailoverPartner(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>參數  
 *伺服器名稱*  
  
 A**字串**包含容錯移轉伺服器名稱。  
  
## <a name="remarks"></a>備註  
 初始連接到主體伺服器若失敗，將使用這個方法所設定的值；在建立初始連接之後，將忽略這個值。 [SetDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)方法應該也可用於搭配使用此方法或將會擲回例外狀況。  
  
 驅動程式不支援在已設定容錯移轉伺服器名稱後指定容錯移轉伺服器的通訊埠編號。 不過，呼叫[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)方法和[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)方法[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)支援方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
