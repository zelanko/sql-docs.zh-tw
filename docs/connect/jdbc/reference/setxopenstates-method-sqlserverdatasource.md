---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e63dbb2ef8864c07bf1deb58e99a08ea70fafdf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67972059"
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
  
  
