---
title: "getScale 方法 (SQLServerParameterMetaData) |Microsoft 文件"
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
- SQLServerParameterMetaData.getScale
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b8d8d9c-74aa-4e6e-88f1-2fc5c74004ae
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: be05360747e2b67de20d6e93823b77629b5bbbac
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getscale-method-sqlserverparametermetadata"></a>getScale 方法 (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取所指定之參數的小數點右邊的位數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getScale(int param)  
```  
  
#### <a name="parameters"></a>參數  
 *param*  
  
 **Int** ，指出參數索引。  
  
## <a name="return-value"></a>傳回值  
 在**int** ，指出指定之參數的小數位數。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getScale 方法是由 java.sql.ParameterMetaData 介面中 getScale 方法指定。  
  
 這個方法會取得小數點右邊的資料行位數。 如果是沒有小數點的型別，這個方法會傳回 "0"。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerParameterMetaData 方法](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 成員](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 類別](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
