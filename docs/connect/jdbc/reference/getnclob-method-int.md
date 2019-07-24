---
title: getNClob 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 10dfa251-9408-469e-ae2a-1acf3917cf47
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 63dbc19502ef0d22362008c67a17448bfa48d7f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981519"
---
# <a name="getnclob-method-int"></a>getNClob 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言，擷取所指定 JDBC **NCLOB** 參數的值來作為 NClob 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.NClob getNClob(int parameterIndex)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterIndex*  
  
 指出參數索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 ANClobobject.  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getNClob 方法是由 java.sql.CallableStatement 介面中的 getNClob 方法指定。  
  
 這個方法只支援抓取**NCHAR**、 **NVARCHAR**、 **NTEXT**和**XML**參數。 對其他資料類型參數呼叫這些方法，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getNClob 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
