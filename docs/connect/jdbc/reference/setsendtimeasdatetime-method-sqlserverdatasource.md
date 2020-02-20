---
title: setSendTimeAsDatetime 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 705a0494-b5e2-43db-940a-1b8cec550cdb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 293667d8e3e06fb5eda7a74fdeed58c89fb0f1ae
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67972966"
---
# <a name="setsendtimeasdatetime-method-sqlserverdatasource"></a>setSendTimeAsDatetime 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  這個方法是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增。  
  
 修改 **sendTimeAsDatetime** 連接屬性的設定。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setSendTimeAsDatetime(boolean sendTimeAsDateTime)  
```  
  
#### <a name="parameters"></a>參數  
 *sendTimeAsDateTime*  
  
 布林值。 當為 true 時，會將 java.sql.Time 值作為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime** 類型傳送給伺服器。 當為 false 時，會將 java.sql.Time 值作為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **time** 類型傳送給伺服器。  
  
## <a name="remarks"></a>備註  
 [SQLServerDataSource.getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md) 會傳回 **sendTimeAsDatetime** 連線屬性的設定。  
  
 如需 **sendTimeAsDatetime** 連接屬性的詳細資訊，請參閱[設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)。  
  
 如需詳細資訊，請參閱[設定 java.sql.Time 值如何傳送給伺服器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
