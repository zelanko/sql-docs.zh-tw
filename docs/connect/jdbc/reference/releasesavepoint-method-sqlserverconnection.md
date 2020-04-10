---
title: releaseSavepoint 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.releaseSavepoint
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b6b625ea-c7ce-4a32-a9e0-6d2b4321bfd8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd402193bf666ca7bacadafb44a177ddda71777b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80904060"
---
# <a name="releasesavepoint-method-sqlserverconnection"></a>releaseSavepoint 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  從目前的交易中，移除指定的 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 物件。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 目前不支援這個方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void releaseSavepoint(java.sql.Savepoint savepoint)  
```  
  
#### <a name="parameters"></a>參數  
 *savepoint*  
  
 要移除的 SavePoint 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此 releaseSavepoint 方法是由 java.sql.Connection 介面中的 releaseSavepoint 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
