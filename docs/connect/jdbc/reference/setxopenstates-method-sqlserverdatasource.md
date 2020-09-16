---
description: setXopenStates 方法 (SQLServerDataSource)
title: setXopenStates 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9723591f-e987-426f-b70a-07f5c70dc094
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 345f243f6fb712208df336207ee408cd7596b296
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450610"
---
# <a name="setxopenstates-method-sqlserverdatasource"></a>setXopenStates 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定 **Boolean** 值，這個值指出是否啟用將 SQL 狀態轉換成 XOPEN 標準狀態。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setXopenStates(boolean xopenStates)  
```  
  
#### <a name="parameters"></a>參數  
 *xopenStates*  
  
 如果啟用將 SQL 狀態轉換成 XOPEN 標準狀態，則為 **true**； 否則為 **false**。  
  
## <a name="remarks"></a>備註  
 如果 xopenStates 屬性設定為 **true**，則 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 會將 SQL 狀態轉換成 XOPEN 相容狀態。 預設值是 **false**，將造成 JDBC 驅動程式產生 SQL 99 狀態碼。 如果 xopenStates 未設定，[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md) 方法就會傳回預設值 **false**。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
