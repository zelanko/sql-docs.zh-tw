---
title: getClientInfoProperties 方法 (SQLServerDatabaseMetaData) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1568aef4-f4c4-40a0-a1ab-9c106905bd92
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e238a9899bd56002d03373ac037b8bd46059b030
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32832903"
---
# <a name="getclientinfoproperties-method-sqlserverdatabasemetadata"></a>getClientInfoProperties 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取此驅動程式支援之用戶端資訊屬性的清單。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getClientInfoProperties()  
```  
  
## <a name="return-value"></a>傳回值  
 結果集物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getClientInfoProperties 方法是由 java.sql.DatabaseMetaData 介面中的 getClientInfoProperties 方法指定。  
  
> [!NOTE]  
>  這個方法會傳回空的結果集。 驅動程式僅支援設定**applicationName**並設定**applicationName**只在連接時間。 SQL Server 不支援在已建立連接之後更新用戶端應用程式資訊。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
