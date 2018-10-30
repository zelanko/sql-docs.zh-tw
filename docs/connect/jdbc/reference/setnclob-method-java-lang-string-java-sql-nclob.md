---
title: setNClob 方法 (java.lang.String, java.sql.NClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4e30d242-0c1b-45db-b75f-41b041692f31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1a94bed36865c55fabc56704766f2a2c1bcd4d8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47736756"
---
# <a name="setnclob-method-javalangstring-javasqlnclob"></a>setNClob 方法 (java.lang.String, java.sql.NClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為所指定 NClob 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setNClob(java.lang.String parameterName,  
              java.sql.NClob value)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterName*  
  
 包含參數名稱的**字串**。  
  
 *value*  
  
 NClob 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個方法應該用於**NCHAR**， **NVARCHAR**， **NTEXT**，以及**XML**參數資料類型。  
  
 這個 setNClob 方法是由 java.sql.CallableStatement 介面中的 setNClob 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [setNClob 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
