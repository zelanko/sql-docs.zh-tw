---
description: getURL 方法 (SQLServerDatabaseMetaData)
title: getURL 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fcb66851-db5f-4ae8-b728-d129480b6f42
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7371c5aa585c7ffc9ec434e8c0dbc5ae6ecc4d89
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433870"
---
# <a name="geturl-method-sqlserverdatabasemetadata"></a>getURL 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫的 URL。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getURL()  
```  
  
## <a name="return-value"></a>傳回值  
 包含 URL 的**字串**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getURL 方法是由 java.sql.DatabaseMetaData 介面中的 getURL 方法所指定。  
  
 當配合 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫使用 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 時，這個方法會傳回包含下列資訊的**字串**值：  
  
-   URL 值，"jdbc:sqlserver://"  
  
-   選擇性的連線屬性，例如 **serverName**、**instanceName** 及 **portNumber**  
  
-   使用者設定的其他連線屬性，以及包含非空白或非 Null 驅動程式預設值的所有連線屬性，但 **userName**、**password** 和 **integratedSecurity** 除外。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
