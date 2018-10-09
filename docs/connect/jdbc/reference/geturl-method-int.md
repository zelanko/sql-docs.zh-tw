---
title: getURL 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getURL Ijnt)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 75d03ced-3614-4997-9abd-24642b1d1aae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e6e9fa2476ac61f5f5de026aa9d629518e9041e6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47837766"
---
# <a name="geturl-method-int"></a>getURL 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式語言，並配合給定的參數索引來擷取指定參數的值當做  物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.net.URL getURL(int n)  
```  
  
#### <a name="parameters"></a>參數  
 *n*  
  
 指出參數索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 URL 的物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setURL 方法由 java.sql.CallableStatement 介面中的 setURL 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [setNull 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/geturl-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
