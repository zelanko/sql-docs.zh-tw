---
title: getServerName 方法 (SQLServerDataSource) |Microsoft 文件
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
- SQLServerDataSource.getServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3004ed22-5d69-4dd0-8761-d39f0b7dde13
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd2d58a2c47553fee1d5c8d4cf9355998078e4d6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getservername-method-sqlserverdatasource"></a>getServerName 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回名稱[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getServerName()  
```  
  
## <a name="return-value"></a>傳回值  
 A**字串**如果未不設定任何值包含伺服器名稱或 null。  
  
## <a name="remarks"></a>備註  
 伺服器名稱是正在執行的目標電腦的主機名稱[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 如果未設定 getServerName 屬性，getservername 會傳回預設值是 null。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
