---
title: getArray 方法 (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getArray (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4610cbaf-5638-4a66-bd83-70aefca40e58
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eefc1d5c3f71618fc448b27c5c91cdb82b12e7b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47778376"
---
# <a name="getarray-method-javalangstring"></a>getArray 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  透過指定的參數名稱，擷取所指定參數的值來作為 Array 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Array getArray(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 陣列物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getArray 方法是由 java.sql.CallableStatement 介面中的 getArray 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [getArray 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getarray-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
