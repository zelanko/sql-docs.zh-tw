---
title: setBinaryStream 方法來輸入資料流) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 339c8277-2d08-4094-9fa9-26c8ad3e7348
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 67b7b7ae7e9e90bab4ad22cbebf248b62351749b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47766778"
---
# <a name="setbinarystream-method-javalangstring-javaioinputstream"></a>setBinaryStream 方法 (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為指定的輸入資料流。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setBinaryStream(java.lang.String parameterName,  
                            java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterName*  
  
 **String**，其中包含參數的名稱。  
  
 *x*  
  
 InputStream 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 setBinaryStream 方法 setBinaryStream 方法 java.sql.CallableStatement 介面中所指定。  
  
## <a name="see-also"></a>另請參閱  
 [setBinaryStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
