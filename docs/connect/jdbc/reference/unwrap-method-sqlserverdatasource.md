---
title: unwrap 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eb8abe29-f3ec-4752-a590-1d5dc3e48f08
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f8cb254ba464b0e051c00c7ac6d410c5e6da1e36
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67997284"
---
# <a name="unwrap-method-sqlserverdatasource"></a>unwrap 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回可實作指定介面的物件，此介面可允許存取 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 特定的方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>參數  
 *iface*  
  
 T 類型的類別，可定義介面。  
  
## <a name="return-value"></a>傳回值  
 物件，可實作指定的介面。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) 方法是由 JDBC 4.0 規格中引進的 java.sql.Wrapper 介面所定義。  
  
 應用程式可能必須存取 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 特定的 JDBC API 延伸模組。 在類別公開供應商延伸模組的情況下，unwrap 方法支援解除包裝為這個物件可擴充的公用類別。  
  
 當呼叫這個方法時，物件會解除包裝成為 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 類別。  
  
 如需詳細資訊，請參閱[包裝函式與介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [isWrapperFor 方法 &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)   
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
