---
title: unwrap 方法 (SQLServerXADataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d97c99b3-2224-4abb-8b32-40aff49fe759
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 51b1b1c5582f87b8f8449f80c48d1a1b24e9cd4f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38052615"
---
# <a name="unwrap-method-sqlserverxadatasource"></a>unwrap 方法 (SQLServerXADataSource)
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
 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) 方法是由 JDBC 4.0 規格中引進的 java.sql.Wrapper 介面所定義。  
  
 應用程式可能必須存取 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 特定的 JDBC API 延伸模組。 在類別公開供應商延伸模組的情況下，unwrap 方法支援解除包裝為這個物件可擴充的公用類別。  
  
 [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md) 類別會擴充 [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) 類別，而後者是由 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 類別擴充所得到的類別。 當呼叫這個方法時，物件會解除包裝為下列類別：[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)、[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) 和 [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)。  
  
 如需詳細資訊，請參閱 <<c0> [ 包裝函式和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXADataSource 方法](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [SQLServerXADataSource 成員](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [SQLServerXADataSource 類別](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
