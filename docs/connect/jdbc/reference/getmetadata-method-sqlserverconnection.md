---
title: getMetaData 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getMetaData
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 86223cb5-3bf4-489a-8c82-669a91764f2b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a51abb4e39b25f11ea1b094232b6f9f4d0badb3f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80906291"
---
# <a name="getmetadata-method-sqlserverconnection"></a>getMetaData 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取 [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 物件，其中包含此 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件表示連接到其中資料庫的相關中繼資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.DatabaseMetaData getMetaData()  
```  
  
## <a name="return-value"></a>傳回值  
 DatabaseMetaData 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getMetaData 方法是由 java.sql.Connection 介面中的 getMetaData 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
