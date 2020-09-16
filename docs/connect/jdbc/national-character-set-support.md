---
description: 國家字元集支援
title: 國家字元集支援 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4fceacfd-df4f-40cd-b7a2-5e5e58a5979f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 394d81f28921bfc4e68204778ed6fcdf1e2fb9e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438340"
---
# <a name="national-character-set-support"></a>國家字元集支援
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  JDBC 驅動程式提供了 JDBC 4.0 API 的支援，其中包含全新的國家字元集轉換 API 方法。 此支援包括適用於 **NCHAR**、**NVARCHAR**、**LONGNVARCHAR** 及 **NCLOB** JDBC 類型的新 setter、getter 和 updater 方法。  
  
 下面是支援國家字元集轉換的新 getter、setter 和 updater 方法清單：  
  
-   [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)：[setNString](../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md)、[setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)、[setNClob](../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)。  
  
-   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)：[getNClob](../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)、[getNString](../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)、[getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)、[setNString](../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md)、[setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)、[setNClob](../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)。  
  
-   [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)：[getNClob](../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)、[getNString](../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)、[getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)、[updateNClob](../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)、[updateNString](../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)、[updateNCharacterStream](../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)。  
  
> [!NOTE]  
>  若要在應用程式中使用這些方法，您必須將 Classpath 設定為包含 sqljdbc4.jar 檔案。  
  
 為了以 Unicode 格式將 String 參數傳送至伺服器，應用程式應該使用新的 JDBC 4.0 國家字元方法，或在使用非國家字元方法時，將 **sendStringParametersAsUnicode** 連線屬性設定為 "**true**"。 建議的方式為盡可能使用新的 JDBC 4.0 國家字元方法。 如需 **sendStringParametersAsUnicode** 連線屬性的詳細資訊，請參閱[設定連線屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [了解 JDBC 驅動程式資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
