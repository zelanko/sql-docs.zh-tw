---
title: getPortNumber 方法 (SQLServerDataSource) |Microsoft Docs
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
ms.openlocfilehash: 7ed56e9a1ece100cc5a8900a2a810bd52b8ab3be
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786435"
---
# <a name="getportnumber-method-sqlserverdatasource"></a>getPortNumber 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回目前用來與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通訊的通訊埠編號。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>傳回值  
 包含目前通訊埠編號的 **int** 值。  
  
## <a name="remarks"></a>Remarks  
 通訊埠編號為 TCP/IP 通訊埠編號，當開啟與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之間的通訊端連線時就會使用此編號。 如果未設定 portNumber 屬性，getPortNumber 方法會傳回預設值 1433。  
  
> [!NOTE]  
>  [SetPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)方法不會執行任何範圍檢查傳入的連接埠值。 您可以傳遞無效的如 99999，而不觸發錯誤編號。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
