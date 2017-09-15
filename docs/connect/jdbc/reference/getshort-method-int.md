---
title: "getShort 方法 (int) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.getShort (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cd9773c1-b598-4adb-aaf6-0c0f589cbef5
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d695ec99eff61ec25ada91273eec6e723463a45f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getshort-method-int"></a>getShort 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取所指定之參數的值**簡短**在 Java 程式語言中使用給定的參數索引。  
  
## <a name="syntax"></a>語法  
  
```  
  
public short getShort(int index)  
```  
  
#### <a name="parameters"></a>參數  
 *索引*  
  
 **Int** ，指出參數索引。  
  
## <a name="return-value"></a>傳回值  
 A**簡短**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetShort 方法 java.sql.CallableStatement 介面中所指定此 getShort 方法。  
  
 這個方法僅支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料型別，可以安全傳回整數值，例如**smallint**， **tinyint**，和**元**。 對任何其他資料類型使用這個方法，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getShort 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
