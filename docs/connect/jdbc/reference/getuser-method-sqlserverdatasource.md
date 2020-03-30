---
title: getUser 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3513dd7f-6ae5-4010-bde0-454ac4365bce
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5562f9b19b59096784ad3dd2a09e9135a7e07cf2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67978181"
---
# <a name="getuser-method-sqlserverdatasource"></a>getUser 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回用來連接到資料來源的使用者名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getUser()  
```  
  
## <a name="return-value"></a>傳回值  
 包含使用者名稱的**字串**。  
  
## <a name="remarks"></a>備註  
 [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) 方法會設定當連線到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體時將要使用的使用者名稱。 如果未設定使用者名稱值，getUser 方法會傳回預設值 null。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
