---
title: "取得驅動程式版本 |Microsoft 文件"
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
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b7578539a178e76796018d2da307381318414cb0
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2018
---
# <a name="getting-the-driver-version"></a>取得驅動程式版本
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  已安裝的版本[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]可以下列方式找到：  
  
-   呼叫[SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)方法[getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md)， [getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md)，或[getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md)。  
  
-   版本會顯示在產品分銷的 readme.txt 檔中。  
  
 此外，JDBC 驅動程式名稱可以從傳回[getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) SQLServerDatabaseMetaData 類別上的方法呼叫。 它會傳回，例如"Microsoft JDBC Driver 6.4 for SQL Server"。  
  
 SQLServerDatabaseMetaData 類別方法的呼叫的輸出範例如下：  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 其中 "xxx.x" 為最終的版本號碼。  
  
## <a name="see-also"></a>另請參閱  
 [診斷 JDBC Driver 問題](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
