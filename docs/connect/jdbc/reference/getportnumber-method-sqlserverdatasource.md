---
title: getPortNumber 方法 (SQLServerDataSource) |Microsoft 文件
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
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61ac4328c0a1da1229e568de52cc2d2c89cec437
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getportnumber-method-sqlserverdatasource"></a>getPortNumber 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回目前用來與通訊的通訊埠編號[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>傳回值  
 **Int**值，包含目前的連接埠號碼。  
  
## <a name="remarks"></a>備註  
 連接埠號碼是開啟的通訊端連接時，會使用 TCP/IP 通訊埠編號[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 如果未設定 portNumber 屬性，getPortNumber 方法會傳回預設值 1433。  
  
> [!NOTE]  
>  [SetPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)方法不會進行任何範圍檢查傳入的連接埠值。 您可以傳遞無效的如 99999，而不觸發錯誤編號。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
