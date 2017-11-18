---
title: "setSelectMethod 方法 (SQLServerDataSource) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setSelectMethod
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7934276d-5ac9-4cbc-a2a0-2c65c93733ac
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76ae74c63ac8cf87d0d7fb58f22f8cd1882d5208
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setselectmethod-method-sqlserverdatasource"></a>setSelectMethod 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定使用之所有結果集所建立的使用這項功能的預設資料指標類型[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setSelectMethod(java.lang.String selectMethod)  
```  
  
#### <a name="parameters"></a>參數  
 *selectMethod*  
  
 A**字串**包含預設資料指標類型的值。  
  
## <a name="remarks"></a>備註  
 selectMethod 是用於結果集的預設資料指標類型。 當您處理大型結果集而且不想要將完整結果集儲存在用戶端的記憶體內時，這個屬性會很實用。 將此屬性設定為 "cursor"，您就可以建立伺服器端資料指標，一次提取較小的資料區塊。 如果未設定 selectMethod 屬性， [getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)會傳回預設值"direct"。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

