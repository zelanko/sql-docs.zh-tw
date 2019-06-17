---
title: setNCharacterStream 方法來讀取器物件-字串 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fd19fbb8-a878-4d98-a584-e4969d649844
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 361193c9f85034da5a40c6dac6d1865a77c34612
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800473"
---
# <a name="setncharacterstream-method-javalangstring-javaioreader"></a>setNCharacterStream 方法 (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為所指定 Reader 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setNCharacterStream(java.lang.String parameterName,  
                       java.io.Reader value)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterName*  
  
 指出參數名稱的**字串**。  
  
 *value*  
  
 讀取器物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 setNCharacterStream 方法是由 java.sql.CallableStatement 介面中的 setNCharacterStream 方法指定。  
  
 這個方法應該用於**NCHAR**， **NVARCHAR**， **NTEXT**，以及**XML**資料型別。  
  
## <a name="see-also"></a>另請參閱  
 [setNCharacterStream 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
