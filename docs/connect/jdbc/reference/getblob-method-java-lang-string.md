---
title: getBlob 方法 (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBlob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3fe74b50-9ccd-4973-a93a-6da2c20a4154
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5cf5ece7dff3a6e749025828ef0886ccb15eabf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47777216"
---
# <a name="getblob-method-javalangstring"></a>getBlob 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言，並配合指定的參數名稱來擷取所指定 JDBC BLOB 參數的值作為 Blob 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Blob getBlob(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 Blob 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getBlob 方法是由 java.sql.CallableStatement 介面中的 getBlob 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [getBlob 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getblob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
