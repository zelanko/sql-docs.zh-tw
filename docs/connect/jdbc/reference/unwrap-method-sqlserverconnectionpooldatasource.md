---
title: 解除包裝方法 (SQLServerConnectionPoolDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f5c9b734-2096-4ae4-a284-6b4d1b4a00d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab408e917a1e6c22cdbe320eb19f5c9995c6e216
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985614"
---
# <a name="unwrap-method-sqlserverconnectionpooldatasource"></a>unwrap 方法 (SQLServerConnectionPoolDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回可實作指定介面的物件，此介面可允許存取 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 特定的方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>參數  
 *iface*  
  
 **T** 類型的類別，可定義介面。  
  
## <a name="return-value"></a>傳回值  
 物件，可實作指定的介面。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md) 方法是由 JDBC 4.0 規格中引進的 java.sql.Wrapper 介面所定義。  
  
 應用程式可能必須存取 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 特定的 JDBC API 延伸模組。 在類別公開供應商延伸模組的情況下，unwrap 方法支援解除包裝為這個物件可擴充的公用類別。  
  
 [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) 類別會擴充 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 類別。 當呼叫這個方法時，物件會解除包裝成為 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 類別和 [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) 類別。  
  
 如需詳細資訊, 請參閱包裝函式[和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnectionPoolDataSource 方法](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [SQLServerConnectionPoolDataSource 成員](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [SQLServerConnectionPoolDataSource 類別](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
