---
title: "國家字元集支援 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4fceacfd-df4f-40cd-b7a2-5e5e58a5979f
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9be09b40e72a19a498913bf824e73b52db6596a2
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="national-character-set-support"></a>國家字元集支援
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  JDBC 驅動程式提供了 JDBC 4.0 API 的支援，其中包含全新的國家字元集轉換 API 方法。 這項支援包括的新 setter、 getter 和 updater 方法**NCHAR**， **NVARCHAR**， **LONGNVARCHAR**，和**NCLOB** JDBC 類型。  
  
 下面是支援國家字元集轉換的新 getter、setter 和 updater 方法清單：  
  
-   [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md): [setNString](../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md)， [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)， [setNClob](../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)。  
  
-   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)， [getNString](../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)， [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)， [setNString](../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md)， [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)， [setNClob](../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)。  
  
-   [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)， [getNString](../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)， [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)， [updateNClob](../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)， [updateNString](../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)， [updateNCharacterStream](../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)。  
  
> [!NOTE]  
>  若要在應用程式中使用這些方法，您必須將 Classpath 設定為包含 sqljdbc4.jar 檔案。  
  
 若要將 String 參數傳送到伺服器以 Unicode 格式，應用程式可以使用新的 JDBC 4.0 國家字元方法;設定或**sendStringParametersAsUnicode**連接屬性設"**true**」 使用非國家字元方法時。 建議的方式為盡可能使用新的 JDBC 4.0 國家字元方法。 如需有關**sendStringParametersAsUnicode**連接屬性，請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
