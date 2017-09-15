---
title: "ISQLServerPreparedStatement 介面 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf87892e-5c34-4ac6-8258-c2a81e117b26
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 56f10262ce0f55434419600299fb12961d9be15b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="isqlserverpreparedstatement-interface"></a>ISQLServerPreparedStatement 介面
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表 JDBC 備妥之陳述式功能的基本實作。 此介面已加入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC 驅動程式 3.0。  
  
 **封裝：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** java.sql.PreparedStatement、 [ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
public interface ISQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>備註  
 這個介面由實作[SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。  
  
 這個介面會公開下列[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-特有的方法：  
  
|方法|如需詳細資訊，請參閱|  
|------------|-------------------------------|  
|public void setDateTimeOffset(int, microsoft.sql.DateTimeOffset)|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlserverpreparedstatement.md)|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
