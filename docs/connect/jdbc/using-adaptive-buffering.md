---
title: 使用適應性緩衝 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 92d4e3be-c3e9-4732-9a60-b57f4d0f7cb7
caps.latest.revision: 53
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0a4d3409d9d87bfaca810405e542130a90a471b
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785735"
---
# <a name="using-adaptive-buffering"></a>使用適應性緩衝

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

適應性緩衝是針對在沒有伺服器資料指標負擔的情況下，擷取任何種類的大數值資料而設計的。 應用程式可以使用自適性緩衝功能搭配此驅動程式所支援的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。

一般而言，當 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 執行查詢時，驅動程式會將伺服器中的所有結果擷取到應用程式記憶體中。 雖然這個方法會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資源耗用量降到最低，但是它會針對產生非常龐大結果的查詢，在 JDBC 應用程式中擲回 OutOfMemoryError。

為了允許應用程式處理非常龐大的結果，因此 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供自適性緩衝。 使用自適性緩衝，此驅動程式會在應用程式需要時，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中擷取陳述式執行結果，而非一次擷取所有結果。 只要應用程式不再存取這些結果，驅動程式也可以捨棄它們。 下面是適應性緩衝可能有用的部分範例：

- **查詢會產生非常龐大的結果集：** 應用程式可以執行 SELECT 陳述式，該陳述式會產生比應用程式可以儲存在記憶體中還要多的資料列。 在舊版中，應用程式必須使用伺服器資料指標來避免 OutOfMemoryError。 適應性緩衝可以針對任意大的結果集進行順向唯讀行程，而不需要伺服器資料指標。

- **此查詢會產生非常龐大的** [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) **資料行或** [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) **OUT 參數值：** 應用程式可以擷取因為過大而無法完整納入應用程式記憶體中的單一值 (資料行或 OUT 參數)。 適應性緩衝可讓用戶端應用程式使用 getAsciiStream、 getBinaryStream 或 getCharacterStream 方法來擷取資料流中，這類值。 應用程式會在從資料流讀取時，擷取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的值。

> [!NOTE]  
> 透過適應性緩衝，JDBC Driver 只會緩衝處理它所需的資料量。 此驅動程式不會提供任何公用方法來控制或限制緩衝區的大小。

## <a name="setting-adaptive-buffering"></a>設定適應性緩衝

自 JDBC Driver 2.0 版開始，此驅動程式的預設行為是 "**adaptive**"。 換言之，若要取得適應性緩衝行為，您的應用程式不需要明確要求適應性行為。 但在 1.2 版中，預設的緩衝模式為 "**full**"，且應用程式必須明確要求自適性緩衝模式。

應用程式可以要求陳述式執行應該使用適應性緩衝的方式有三種：

- 應用程式可以設定連接屬性**responseBuffering**為"adaptive"。 如需有關設定連接屬性的詳細資訊，請參閱 <<c0> [ 設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。

- 應用程式可以使用 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 物件的 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md) 方法，設定透過該 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 物件建立之所有連線的回應緩衝模式。

- 應用程式可以使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 類別的 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法來設定特定陳述式物件的回應緩衝模式。

使用 JDBC Driver 1.2 版時，應用程式原本必須將陳述式物件轉換成 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 類別，才能使用 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法。 中的程式碼範例[讀取大型資料範例](../../connect/jdbc/reading-large-data-sample.md)並[讀取大型資料與預存程序範例](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md)示範這個舊的使用方式。

不過，使用 JDBC Driver 2.0 版時，應用程式可以使用 [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) 方法和 [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 方法來存取供應商特定的功能，而不需要提出有關實作類別階層的任何假設。 取得範例程式碼，請參閱 <<c0> [ 更新大型資料範例](../../connect/jdbc/updating-large-data-sample.md)主題。

## <a name="retrieving-large-data-with-adaptive-buffering"></a>利用適應性緩衝擷取大型資料

使用 get\<類型>Stream 方法讀取大數值一次，而且以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回的順序存取 ResultSet 資料行和 CallableStatement OUT 參數時，自適性緩衝會將處理結果時的應用程式記憶體使用量降到最低。 使用適應性緩衝時：

- 雖然資料流透過應用程式標示時可以重設，但是在 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 類別中定義的 get\<類型>Stream 方法預設還是會傳回讀取一次的資料流。 如果應用程式想要 `reset` 資料流，必須先在該資料流上呼叫 `mark` 方法。

- 在 [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) 和 [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) 類別中定義的 get\<類型>Stream 方法會傳回一律可以重新定位到資料流開始位置的資料流，而不需要呼叫 `mark` 方法。

當應用程式使用自適性緩衝時，僅可以擷取 get\<類型>Stream 方法所擷取值一次。 如果您在呼叫相同物件的 get\<類型>Stream 方法後，嘗試針對相同的資料行或參數呼叫任何 get\<類型> 方法，則會擲回例外狀況並顯示訊息：「資料已存取，此資料行或參數無法使用」。

> [!NOTE]
> 處理結果集的中間呼叫 ResultSet.close() 需要 Microsoft JDBC Driver for SQL Server 讀取，並捨棄其餘的所有封包。 如果查詢傳回大型資料集，尤其是網路連線速度很慢，這可能需要相當的時間。

## <a name="guidelines-for-using-adaptive-buffering"></a>使用適應性緩衝的指導方針

開發人員應該遵循這些重要的指導方針，將應用程式的記憶體使用量降到最低：

- 請避免使用 **selectMethod=cursor** 連接字串屬性，以讓應用程式處理非常龐大的結果集。 適應性緩衝功能可讓應用程式處理非常大的順向唯讀結果集，而不需要使用伺服器資料指標。 請注意，當您設定 **selectMethod=cursor** 時，該連線產生的所有順向唯讀結果集都會受到影響。 換言之，如果您的應用程式例行地處理含有少數資料列的簡短結果集，就用戶端和伺服器端而言，針對每個結果集建立、讀取和關閉伺服器資料指標所使用的資源會比 **selectMethod** 沒有設定為 **cursor** 的情況還多。

- 為資料流將大型文字或二進位值讀取使用 getAsciiStream、 getBinaryStream 或 getCharacterStream 方法，而不是 getBlob 或 getClob 方法中。 從 1.2 版開始，[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 類別會針對此用途提供新的 get\<類型>Stream 方法。

- 確保潛在具有大數值的資料行放置在 SELECT 陳述式之資料行清單中的最後面，並確保 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 的 get\<類型>Stream 方法用於以選取的順序存取資料行。

- 確保潛在具有大數值的 OUT 參數在用於建立 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 之 SQL 中的參數清單結尾處宣告。 此外，確保 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 的 get\<類型>Stream 方法用於以宣告的順序存取 OUT 參數。

- 避免在相同的連接上，同時執行一個以上的陳述式。 在處理前一個陳述式的結果前執行其他陳述式可能會使未處理的結果在應用程式記憶體中緩衝處理。

- 有某些情況下，使用**selectMethod = cursor**而不是**responseBuffering = adaptive**會更有效率，例如：

  - 如果您的應用程式處理順向、 唯讀結果集速度緩慢，例如在使用某些使用者輸入之後讀取每個資料列**selectMethod = cursor**而不是**responseBuffering = adaptive**可能減少所使用的資源[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

  - 如果您的應用程式針對相同的連線同時處理兩個以上的順向唯讀結果集，請使用 **selectMethod=cursor** 而非 **responseBuffering=adaptive** 可能會有助於減少驅動程式在處理這些結果集時所需的記憶體。

  在這兩種情況下，您必須考慮建立、讀取和關閉伺服器資料指標的負擔。

此外，下列清單將針對可捲動和順向可更新的結果集提供一些建議事項：

- 若為可捲動的結果集，在提取資料列的區塊時，此驅動程式一定會將 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 物件之 [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) 方法所指定的資料列數目讀入記憶體中，即使已啟用自適性緩衝也一樣。 如果捲動導致 OutOfMemoryError，您可以呼叫 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的 [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) 方法，將提取大小設定為更小的資料列數目 (必要時，甚至可以降低至 1 個資料列)，藉此減少所提取的資料列數目。 如果這樣做無法防止 OutOfMemoryError，請避免在可捲動的結果集中包含非常龐大的資料行。

- 若為順向可更新的結果集，在提取資料列的區塊時，此驅動程式通常會將 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 物件之 [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) 方法所指定的資料列數目讀入記憶體中，即使連線已啟用自適性緩衝也一樣。 如果呼叫 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的 [next](../../connect/jdbc/reference/next-method-sqlserverresultset.md) 方法導致 OutOfMemoryError，您可以呼叫 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的 [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) 方法，將提取大小設定為更小的資料列數目 (必要時，甚至可以降低至 1 個資料列)，藉此減少所提取的資料列數目。 此外，您也可以在執行陳述式之前，呼叫 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 物件的 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法並搭配 "**adaptive**" 參數，藉此強制驅動程式不要緩衝處理任何資料列。 因為結果集並非可捲動，所以如果應用程式使用其中一個 get\<類型>Stream 方法來存取大型資料行值，此驅動程式就會在應用程式讀取該值時捨棄它，就如同針對順向唯讀結果集所做的一樣。

## <a name="see-also"></a>另請參閱

[善 JDBC Driver 的效能與可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
