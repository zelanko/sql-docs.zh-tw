---
title: setClob 方法 (java.lang.String, java.sql.Clob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 256b5f55-7a6d-44fb-9a09-19fa39f19c35
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b76a8cbf6e0946c90dbf6033d5276f475f3123ca
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974891"
---
# <a name="setclob-method-javalangstring-javasqlclob"></a>setClob 方法 (java.lang.String, java.sql.Clob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為所指定 Clob 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setClob(java.lang.String parameterName,  
            java.sql.Clob x)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterName*  
  
 包含參數名稱的**字串**。  
  
 *x*  
  
 Clob 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setClob 方法是由 java.sql.CallableStatement 介面中的 setClob 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [setClob 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
