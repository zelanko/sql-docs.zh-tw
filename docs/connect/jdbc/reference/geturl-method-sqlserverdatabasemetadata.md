---
title: getURL 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0372cab3f29733306262e7986d2dd8e407e78564
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47768608"
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
  
## <a name="remarks"></a>Remarks  
 這個 getURL 方法是由 java.sql.DatabaseMetaData 介面中的 getURL 方法所指定。  
  
 當配合 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫使用 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 時，這個方法會傳回包含下列資訊的**字串**值：  
  
-   URL 值，"jdbc:sqlserver://"  
  
-   選擇性的連接屬性，例如**serverName**， **instanceName**，和**連接埠號碼**  
  
-   使用者設定的其他連線屬性，以及包含非空白或非 Null 驅動程式預設值的所有連線屬性，但 **userName**、**password** 和 **integratedSecurity** 除外。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
