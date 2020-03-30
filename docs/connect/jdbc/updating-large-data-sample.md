---
title: 更新大型資料範例 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76ecc05f-a77d-40a2-bab9-91a7fcf17347
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 231125f60ec0c5791e55a10cff56b3b93339fb91
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027075"
---
# <a name="updating-large-data-sample"></a>更新大型資料範例

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 範例應用程式示範如何更新資料庫中的大型資料行。

此範例的程式碼檔案名稱為 UpdateLargeData.java，可在下列位置找到：

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>需求

若要執行此範例應用程式，您必須存取 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫。 您也必須將 Classpath 設定為包含 sqljdbc4.jar 檔案。 如果 Classpath 遺漏 sqljdbc4.jar 的項目，範例應用程式將會擲回「找不到類別」的一般例外狀況。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../connect/jdbc/using-the-jdbc-driver.md)。

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供 sqljdbc.jar、sqljdbc4.jar、sqljdbc41.jar 或 sqljdbc42.jar 類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定來使用。 此範例會使用 JDBC 4.0 API 中導入的 [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) 和 [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 方法來存取驅動程式特有的回應緩衝方法。 若要編譯並執行此範例，您將需要使用 sqljdbc4.jar 類別庫，以便提供 JDBC 4.0 的支援。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱 [JDBC Driver 的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。

## <a name="example"></a>範例

在下列範例中，範例程式碼會建立與 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 資料庫的連線。 然後，範例程式碼會建立 Statement 物件並使用 [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) 方法來檢查此 Statement 物件是否為指定之 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 類別的包裝函式。 [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 方法用來存取驅動程式特有的回應緩衝方法。

接下來，範例程式碼會使用 **SQLServerStatement** 類別的 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法，將回應緩衝模式設定為 "[adaptive](../../connect/jdbc/reference/sqlserverstatement-class.md)"，而且也將示範如何取得自適性緩衝模式。

然後，它會執行 SQL 陳述式，並且將所傳回的資料放入可更新的 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中。

最後，範例程式碼會逐一查看結果集中的資料列。 如果它找到空的文件摘要，就會使用 [updateString](../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) 與 [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 方法的組合來更新資料列，並且再次將資料保存在資料庫中。 如果已經存在資料，它就會使用 [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) 方法來顯示部分資料。

此驅動程式的預設行為是 "**adaptive**"。 不過，若為順向可更新結果集，而且結果集中的資料大小超過應用程式記憶體時，應用程式就必須使用 [SQLServerStatement](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 類別的 [setResponseBuffering](../../connect/jdbc/reference/sqlserverstatement-class.md) 方法來明確設定自適性緩衝模式。

[!code[JDBC#UsingAdaptiveBuffering3](../../connect/jdbc/codesnippet/Java/updating-large-data-sample_1.java)]

## <a name="see-also"></a>另請參閱

[使用大型資料](../../connect/jdbc/working-with-large-data.md)
