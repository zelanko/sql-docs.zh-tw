---
title: 讀取大型資料範例 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6c986144-3854-4352-8331-e79eccbefc28
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0037ee678766bad6786a6feb14e0bf569f9448a0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="reading-large-data-sample"></a>讀取大型資料範例
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  這[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]範例應用程式示範如何擷取大型單一資料行值從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫使用[getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)方法。  
  
 此範例的程式碼檔案名稱為 readLargeData.java，可以在下列位置找到：  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \samples\adaptive  
  
## <a name="requirements"></a>需求  
 若要執行此範例應用程式，您必須存取 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫。 您也必須將 Classpath 設定為包含 sqljdbc.jar 檔案或 sqljdbc4.jar 檔案。 如果 Classpath 遺漏 sqljdbc.jar 或 sqljdbc4.jar 的項目，範例應用程式將會擲回「找不到類別」的一般例外狀況。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供 sqljdbc.jar 和 sqljdbc4.jar 類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定使用。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱[JDBC 驅動程式的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>範例  
 在下列範例中，範例程式碼會建立與 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 資料庫的連線。 接著，範例程式碼會建立範例資料，並使用參數化查詢更新 Production.Document 資料表。  
  
 此外，程式碼範例示範如何取得適應性緩衝模式使用[getResponseBuffering](../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)類別。 請注意，從 JDBC Driver 2.0 版開始，responseBuffering 連接屬性預設設定為 "adaptive"。  
  
 然後，使用 SQL 陳述式與[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)物件，範例程式碼執行 SQL 陳述式與放置資料，它會傳回成[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
 最後，範例程式碼，逐一查看結果集中包含的資料列並使用[getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)方法來存取它所包含的資料部分。  
  
 [!code[JDBC#UsingAdaptiveBuffering1](../../connect/jdbc/codesnippet/Java/reading-large-data-sample_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [使用大型資料](../../connect/jdbc/working-with-large-data.md)  
  
  
