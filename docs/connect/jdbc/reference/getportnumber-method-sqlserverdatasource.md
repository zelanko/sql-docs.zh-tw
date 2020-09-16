---
description: getPortNumber 方法 (SQLServerDataSource)
title: getPortNumber 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ded903bb6696c3dfefd51979d37605af899b6d6d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435010"
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
  
## <a name="remarks"></a>備註  
 通訊埠編號為 TCP/IP 通訊埠編號，當開啟與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之間的通訊端連線時就會使用此編號。 如果未設定 portNumber 屬性，getPortNumber 方法會傳回預設值 1433。  
  
> [!NOTE]  
>  [setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md) 方法不會針對傳入的連接埠值進行任何範圍檢查。 您可以在不觸發錯誤的情況下傳遞無效的侵權號碼，例如 99999。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
