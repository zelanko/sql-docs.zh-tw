---
title: 取得驅動程式版本 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7abc69edd0d49264a62ea0c3f65a60b58549d105
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47774216"
---
# <a name="getting-the-driver-version"></a>取得驅動程式版本
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  您可以下列方式尋找已安裝的 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 版本：  
  
-   呼叫 [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 方法 [getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md)、[getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md) 或 [getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md)。  
  
-   版本會顯示在產品分銷的 readme.txt 檔中。  
  
 此外，JDBC 驅動程式名稱可從 SQLServerDatabaseMetaData 類別上的 [getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) 方法呼叫傳回。 例如，它會傳回 "Microsoft JDBC Driver 6.4 for SQL Server"。  
  
 SQLServerDatabaseMetaData 類別方法呼叫的輸出範例如下：  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 其中 "xxx.x" 為最終的版本號碼。  
  
## <a name="see-also"></a>另請參閱  
 [診斷 JDBC Driver 問題](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
