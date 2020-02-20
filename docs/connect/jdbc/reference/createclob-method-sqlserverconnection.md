---
title: createClob 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 58b0865a-1cde-4046-9761-51e471294023
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 417a5048d809cb4498c543c589324e151a843a18
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67955403"
---
# <a name="createclob-method-sqlserverconnection"></a>createClob 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  直接建立 Clob 物件，而不使用任何資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Clob createClob()  
```  
  
## <a name="return-value"></a>傳回值  
 Clob 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 createClob 方法是由 java.sql.Connection 介面中的 createClob 方法指定。  
  
 此方法會取代使用 [SQLServerClob 建構函式 &#40;SQLServerConnection, java.lang.String&#41;](../../../connect/jdbc/reference/sqlserverclob-constructor-sqlserverconnection-java-lang-string.md) 的需求。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
