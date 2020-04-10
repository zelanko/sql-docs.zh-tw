---
title: setFailoverPartner 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5310b7c2-9d10-474f-ad3a-218fe5da694b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 58604614f5f5025e0e0982f7d191868e3baf23e0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922333"
---
# <a name="setfailoverpartner-method-sqlserverdatasource"></a>setFailoverPartner 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定用於資料庫鏡像組態的容錯移轉伺服器名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setFailoverPartner(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>參數  
 *serverName*  
  
 **String**，包含容錯移轉伺服器的名稱。  
  
## <a name="remarks"></a>備註  
 初始連接到主體伺服器若失敗，將使用這個方法所設定的值；在建立初始連接之後，將忽略這個值。 結合這個方法時也應該要使用 [setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md) 方法，否則會擲回例外狀況。  
  
 驅動程式不支援在已設定容錯移轉伺服器名稱後指定容錯移轉伺服器的通訊埠編號。 不過，支援配合 [setFailoverPartner](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md) 方法來呼叫 [setServerName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md) 方法和 [setInstanceName](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
