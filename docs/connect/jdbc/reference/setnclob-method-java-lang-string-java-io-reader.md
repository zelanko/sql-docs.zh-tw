---
title: "setNClob 方法 （java.lang.String，java.io.Reader） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a595679a-89b7-4b18-9ad2-d9cb13af2a28
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 526afd5d4b5af7cf58e3c975159ab037425b908a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setnclob-method-javalangstring-javaioreader"></a>setNClob 方法 (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定之的參數設定為指定的讀取器物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setNClob(java.lang.String parameterName,  
              java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>參數  
 *參數名稱*  
  
 A**字串**，其中包含參數名稱。  
  
 *讀取器*  
  
 讀取器物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個方法應用於**NCHAR**， **NVARCHAR**， **NTEXT**，和**XML**參數資料類型。  
  
 SetNClob 方法 java.sql.CallableStatement 介面中所指定此 setNClob 方法。  
  
## <a name="see-also"></a>另請參閱  
 [setNClob 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  

