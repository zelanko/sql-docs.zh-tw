---
title: setFloat 方法 (SQLServerCallableStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setFloat
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 26d861da-bb6a-4197-8b32-13dc7781c2bb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caee7a8263997955b1199b906c6ac216bed4cd66
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722946"
---
# <a name="setfloat-method-sqlservercallablestatement"></a>setFloat 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為指定的 Java 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setFloat(java.lang.String sCol,  
                     float f)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
 *-f*  
  
 A**浮點數**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setURL 方法由 java.sql.CallableStatement 介面中的 setURL 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
