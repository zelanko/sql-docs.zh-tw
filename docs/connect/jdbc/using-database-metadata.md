---
title: 使用資料庫中繼資料 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b2f3e0a4e19b30eeb494f89281a01195cf98b7d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32850663"
---
# <a name="using-database-metadata"></a>使用資料庫中繼資料
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要查詢資料庫有關，支援什麼[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]實作[SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)類別。 此類別包含數種方法，會以單一值形式或以結果集傳回資訊。  
  
 若要建立 SQLServerDatabaseMetaData 物件時，您可以使用[getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)類別，以取得連接到資料庫的相關資訊。  
  
 在下列範例中，開啟連接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式、 SQLServerConnection 類別的 getMetaData 方法用來傳回 SQLServerDatabaseMetadata 物件，以及然後各種方法SQLServerDatabaseMetaData 物件可用來顯示驅動程式、 驅動程式版本、 資料庫名稱和資料庫版本的相關資訊。  
  
 [!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [使用 JDBC Driver 處理中繼資料](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  
