---
title: "getFailoverPartner 方法 (SQLServerDataSource) |Microsoft 文件"
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
- SQLServerDataSource.getFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 885f927f-9c48-42e0-a7fb-fd936d2b8130
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f2b5076573d1513313949a5ad9b558a24315bf5c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getfailoverpartner-method-sqlserverdatasource"></a>getFailoverPartner 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回用於資料庫鏡像組態的容錯移轉伺服器名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public string getFailoverPartner()  
```  
  
## <a name="return-value"></a>傳回值  
 A**字串**，其中包含的容錯移轉夥伴或為 null 的名稱，如果沒有設定。  
  
## <a name="remarks"></a>備註  
 容錯移轉夥伴名稱設定使用這個方法所傳回的值會反映[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

