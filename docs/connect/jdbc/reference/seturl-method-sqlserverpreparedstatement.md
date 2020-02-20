---
title: setURL 方法 (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d853b2f3-fb72-4d4b-8997-f4a45a9dfefc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 47b1cff27860a09e4f9b8cc43f8523b5a1846a3c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67972083"
---
# <a name="seturl-method-sqlserverpreparedstatement"></a>setURL 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為給定的 URL 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setURL(int parameterIndex,  
                         java.net.URL x)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterindex*  
  
 **int**，指出參數編號。  
  
 *x*  
  
 URL 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setURL 方法是由 java.sql.PreparedStatement 介面中的 setURL 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
