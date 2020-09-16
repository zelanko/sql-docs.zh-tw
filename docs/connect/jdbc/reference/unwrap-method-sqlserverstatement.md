---
description: unwrap 方法 (SQLServerStatement)
title: unwrap 方法 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce680176-ef04-4e44-bb6c-ec50bd06e7e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 792bd67690453bbef4ac77dae8910b103eab2957
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458060"
---
# <a name="unwrap-method-sqlserverstatement"></a>unwrap 方法 (SQLServerStatement)
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
  
## <a name="remarks"></a>備註  
 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 方法是由 JDBC 4.0 規格中引進的 java.sql.Wrapper 介面所定義。  
  
 應用程式可能必須存取 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 特定的 JDBC API 延伸模組。 在類別公開供應商延伸模組的情況下，unwrap 方法支援解除包裝為這個物件可擴充的公用類別。  
  
 當呼叫這個方法時，物件會解除包裝成為 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 類別。  
  
 如需範例程式碼，請參閱[更新大型資料範例](../../../connect/jdbc/updating-large-data-sample.md)，或 [unwrap 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)。  
  
 如需詳細資訊，請參閱[包裝函式與介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [isWrapperFor 方法 &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)   
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
