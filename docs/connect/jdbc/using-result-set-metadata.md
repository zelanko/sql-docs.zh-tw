---
title: 使用結果集中繼資料 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ea7ce7da7d5327c12204d60ec5c97ec58793403
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38041414"
---
# <a name="using-result-set-metadata"></a>使用結果集中繼資料
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  為了查詢結果集內所包含之資料行的資訊，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會實作 [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) 類別。 此類別包含數種以單一值形式傳回資訊的方法。  
  
 若要建立 SQLServerResultSetMetaData 物件時，您可以使用[getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)類別。  
  
 在下列範例中，開啟連線[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式、 SQLServerResultSet 類別的 getMetaData 方法來傳回 SQLServerResultSetMetaData 物件，並接著的各種方法SQLServerResultSetMetaData 物件用來顯示結果集內包含資料行的名稱和資料類型的相關資訊。  
  
 [!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [使用 JDBC Driver 處理中繼資料](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  
