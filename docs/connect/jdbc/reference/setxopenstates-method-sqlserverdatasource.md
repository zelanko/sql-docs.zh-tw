---
title: setXopenStates 方法 (SQLServerDataSource) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 65fde7feacb27f8c3b7fb2d809de4f75bc7e899c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695866"
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
  
## <a name="remarks"></a>Remarks  
 如果 xopenStates 屬性設定為 **true**，則 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 會將 SQL 狀態轉換成 XOPEN 標準狀態。 預設值是 **false**，將造成 JDBC 驅動程式產生 SQL 99 狀態碼。 如果 xopenStates 未設定，[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md) 方法就會傳回預設值 **false**。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
