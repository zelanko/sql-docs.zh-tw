---
title: getNCharacterStream 方法 (java.lang.String) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 45d2695b-0727-419d-8921-a51d6feef0aa
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 865cfa04eb93529cdfb792f78cc5ef2e89994f39
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getncharacterstream-method-javalangstring"></a>getNCharacterStream 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取指定之參數的值為給定的參數名稱的讀取器物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLabel*  
  
 A**字串**，其中包含資料行標籤。  
  
## <a name="return-value"></a>傳回值  
 AReaderobject。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個方法應該用來存取**NCHAR**， **NVARCHAR**和**LONGNVARCHAR**參數。  
  
 GetNCharacterStream 方法 java.sql.CallableStatement 介面中所指定此 getNCharacterStream 方法。  
  
## <a name="see-also"></a>另請參閱  
 [getNCharacterStream 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
