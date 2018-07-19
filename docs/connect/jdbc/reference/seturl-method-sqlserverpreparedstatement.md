---
title: setURL 方法 (SQLServerPreparedStatement) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d853b2f3-fb72-4d4b-8997-f4a45a9dfefc
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3619d063f76e5110407ac7f2b742e447ebaf14d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32845833"
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
  
 **Int** ，指出參數編號。  
  
 *x*  
  
 URL 的物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setURL 方法是由 java.sql.PreparedStatement 介面中 setURL 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
