---
title: setServerName 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 70920828-eda0-4064-be9f-c1e460db8f00
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a3c099e8bd441ee263202499036e25c738c9898f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66767980"
---
# <a name="setservername-method-sqlserverdatasource"></a>setServerName 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定正在執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的電腦名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setServerName(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>參數  
 *serverName*  
  
 包含伺服器名稱的**字串**。  
  
## <a name="remarks"></a>Remarks  
 伺服器名稱是正在執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 目標電腦的主機名稱。 如果未設定 serverName 屬性，[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md) 會傳回預設值 null。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
