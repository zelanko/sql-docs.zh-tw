---
title: 讀取大型資料範例 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6c986144-3854-4352-8331-e79eccbefc28
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cc18dbddf98e41957e0b9e47058a0eab2f65fba9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957183"
---
# <a name="reading-large-data-sample"></a>讀取大型資料範例

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

此 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 範例應用程式示範如何使用 [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 方法，從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中擷取大型單一資料行值。

此範例的程式碼檔案名稱為 ReadLargeData.java，可在下列位置找到：

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>需求

若要執行此範例應用程式，您必須存取 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 範例資料庫。 請您也將 classpath 設定為包含 mssql-jdbc jar 檔案。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../../connect/jdbc/using-the-jdbc-driver.md)。

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 提供 mssql-jdbc 類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定來使用。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱 [JDBC Driver 的系統需求](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。

## <a name="example"></a>範例

在下列範例中，範例程式碼會建立與 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 資料庫的連線。 接著，範例程式碼會建立範例資料，並使用參數化查詢更新 Production.Document 資料表。

此外，範例程式碼示範如何使用 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 類別的 [getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) 方法來取得自適性緩衝模式。 請注意，從 JDBC Driver 2.0 版開始，responseBuffering 連接屬性預設設定為 "adaptive"。

然後，搭配 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件使用 SQL 陳述式時，範例程式碼會執行 SQL 陳述式，並且將所傳回的資料放入 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中。

最後，範例程式碼會逐一查看結果集中的資料列，然後使用 [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 方法來存取部分資料。

[!code[JDBC#UsingAdaptiveBuffering1](../../../connect/jdbc/codesnippet/Java/reading-large-data-sample_1.java)]

## <a name="see-also"></a>另請參閱

[使用大型資料](../../../connect/jdbc/code-samples/working-with-large-data.md)
