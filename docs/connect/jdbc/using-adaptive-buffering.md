---
title: 使用適應性緩衝 |Microsoft 文件
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
ms.openlocfilehash: ae4120b567d876556c29254eae65d4471ab63924
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-adaptive-buffering"></a>使用適應性緩衝
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  適應性緩衝是針對在沒有伺服器資料指標負擔的情況下，擷取任何種類的大數值資料而設計的。 應用程式可以使用適應性緩衝功能，所有版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]由驅動程式支援。  
  
 通常，當[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]執行查詢時，驅動程式的所有結果從伺服器擷取到應用程式記憶體。 雖然這種方法資源消耗降[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，它可以針對產生非常龐大的結果的查詢，而 JDBC 應用程式中擲回 OutOfMemoryError。  
  
 為了允許應用程式處理非常龐大的結果，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供了適應性緩衝。 利用適應性緩衝，驅動程式會擷取從陳述式執行結果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]應用程式需要時，而非一次。 只要應用程式不再存取這些結果，驅動程式也可以捨棄它們。 下面是適應性緩衝可能有用的部分範例：  
  
-   **此查詢會產生非常龐大的結果集：**應用程式可以執行產生比應用程式可以儲存在記憶體中的資料列的 SELECT 陳述式。 在舊版中，應用程式必須使用伺服器資料指標，以避免 OutOfMemoryError。 適應性緩衝可以針對任意大的結果集進行順向唯讀行程，而不需要伺服器資料指標。  
  
-   **此查詢會產生非常大**[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)**資料行或**[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)**OUT 參數值：**應用程式可以擷取單一值 (資料行或 OUT 參數) 太大而無法完整納入應用程式的記憶體。         適應性緩衝可讓用戶端應用程式使用 getAsciiStream、 getBinaryStream 或 getCharacterStream 方法擷取資料流，這類值。 應用程式擷取的值從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]從資料流讀取。  
  
> [!NOTE]  
>  透過適應性緩衝，JDBC Driver 只會緩衝處理它所需的資料量。 此驅動程式不會提供任何公用方法來控制或限制緩衝區的大小。  
  
## <a name="setting-adaptive-buffering"></a>設定適應性緩衝  
 從 JDBC 驅動程式 2.0 版中，驅動程式的預設行為是"**適應性**"。 換言之，若要取得適應性緩衝行為，您的應用程式不需要明確要求適應性行為。 在 1.2 版中，不過的緩衝模式為"**完整**」 預設和應用程式，必須明確要求適應性緩衝模式。  
  
 應用程式可以要求陳述式執行應該使用適應性緩衝的方式有三種：  
  
-   應用程式可以設定連接屬性**responseBuffering**為"adaptive"。 如需有關設定連接屬性的詳細資訊，請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
-   應用程式可以使用[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)方法[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)物件來設定的回應緩衝模式，透過建立之所有連接[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)物件。  
  
-   應用程式可以使用[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)類別來設定的回應緩衝模式的特定陳述式物件。  
  
 使用 JDBC Driver 1.2 版，將陳述式物件轉換成所需的應用程式時[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)類別，以使用[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法。 中的程式碼範例[讀取大型資料範例](../../connect/jdbc/reading-large-data-sample.md)和[讀取大型資料與預存程序範例](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md)示範這個舊的使用方式。  
  
 不過，使用 JDBC 驅動程式 2.0 版時，應用程式可以使用[isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)方法和[unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)方法來存取有關的特定廠商功能，而不會提出任何假設實作類別階層架構。 如需範例程式碼，請參閱[更新大型資料範例](../../connect/jdbc/updating-large-data-sample.md)主題。  
  
## <a name="retrieving-large-data-with-adaptive-buffering"></a>利用適應性緩衝擷取大型資料  
 當大型值讀取一次使用 get\<類型 > 所傳回的順序存取資料流方法的結果集資料行和 CallableStatement OUT 參數[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，適應性緩衝，最小化應用程式處理結果時的記憶體使用量。 使用適應性緩衝時：  
  
-   Get\<類型 > 傳送資料流中定義的方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別預設會傳回讀取一次資料流，雖然如果可以重設資料流標記應用程式。 如果在應用程式要`reset`資料流，它必須呼叫`mark`方法的第一次資料流。  
  
-   Get\<類型 > 傳送資料流中定義的方法[SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md)和[SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md)類別會傳回永遠可以重新定位的資料流到不含資料流的開始位置呼叫`mark`方法。  
  
 當應用程式使用適應性緩衝，get 擷取的值\<類型 > 的資料流的方法可以只擷取一次。 如果您嘗試呼叫任何 get\<類型 > 上相同的資料行或參數之後呼叫 get 方法\<類型 > 的資料流物件的方法相同，例外狀況會擲回訊息: 「 資料已存取，不適用於這資料行或參數 」。  
  
> [!NOTE]
> 處理結果集的中間呼叫 ResultSet.close() 需要 Microsoft JDBC Driver for SQL Server 讀取並捨棄所有剩餘的封包。 如果查詢傳回大型資料集，特別是當網路連接相當緩慢，這可能需要相當的時間。     
  
## <a name="guidelines-for-using-adaptive-buffering"></a>使用適應性緩衝的指導方針  
 開發人員應該遵循這些重要的指導方針，將應用程式的記憶體使用量降到最低：  
  
-   請避免使用連接字串屬性**selectMethod = cursor**若要讓應用程式處理非常龐大的結果設定。 適應性緩衝功能可讓應用程式處理非常大的順向唯讀結果集，而不需要使用伺服器資料指標。 請注意，當您設定**selectMethod = cursor**、 所有順向的該連接所產生的唯讀結果集都會受到影響。 換句話說，如果您的應用程式例行地處理含有少數資料列簡短結果集，建立、 讀取和關閉每個結果集都會使用更多資源用戶端和伺服器端上的而不是大小寫的伺服器資料指標位置**selectMethod**未設定為**游標**。  
  
-   以資料流將大型文字或二進位值讀取使用 getAsciiStream、 getBinaryStream 或 getCharacterStream 方法，而不是 getBlob 或 getClob 方法中。 從 1.2 版，開始[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別會提供新的 get\<類型 > 傳送資料流為此目的的方法。  
  
-   確保潛在具有大數值資料行上一次，SELECT 陳述式中的資料行清單中取得\<類型 > 傳送資料流的方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)用來存取中的資料行選取的順序。  
  
-   請確定的 OUT 參數潛在具有大數值是清單中最後宣告用來建立 SQL 中的參數[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)。 此外，請確認 get\<類型 > 傳送資料流的方法[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)用來存取 OUT 參數在宣告它們的順序。  
  
-   避免在相同的連接上，同時執行一個以上的陳述式。 在處理前一個陳述式的結果前執行其他陳述式可能會使未處理的結果在應用程式記憶體中緩衝處理。  
  
-   有某些情況下使用**selectMethod = cursor**而不是**responseBuffering = adaptive**會更有效率，例如：  
  
    -   如果您的應用程式處理順向、 唯讀結果集很慢，例如在使用部分使用者輸入之後讀取每個資料列**selectMethod = cursor**而不是**responseBuffering = adaptive**可能減少所使用的資源[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   如果您的應用程式處理兩個或更順向且唯讀結果集在相同的連接上同時，使用**selectMethod = cursor**而不是**responseBuffering = adaptive**可以幫助減少在處理這些結果集時，驅動程式所需的記憶體。  
  
     在這兩種情況下，您必須考慮建立、讀取和關閉伺服器資料指標的負擔。  
  
 此外，下列清單將針對可捲動和順向可更新的結果集提供一些建議事項：  
  
-   可捲動的結果集，在提取資料列的區塊驅動程式一律會讀入記憶體中所指定的資料列數目時，針對[getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)物件，即使已啟用適應性緩衝。 如果捲動導致 OutOfMemoryError，您可以減少藉由呼叫提取的資料列數目[setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)要將提取大小設定為更小的數目的資料列，物件即使至 1 個資料列，如有必要。 如果這樣做無法防止 OutOfMemoryError，避免在可捲動的結果集中包含非常龐大的資料行。  
  
-   順向可更新的結果集，通常提取資料列的區塊驅動程式會讀入記憶體中所指定的資料列數目時[getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)物件，即使當已啟用適應性緩衝連接上。 如果呼叫[下一步](../../connect/jdbc/reference/next-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)物件 OutOfMemoryError 導致，您可以減少藉由呼叫提取的資料列數目[setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)方法的[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)將提取大小為較少的資料列，即使至 1 個資料列，如有必要的物件。 您也可以強制驅動程式不要緩衝處理任何資料列，藉由呼叫[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)物件具有"**適應性**"之前的參數執行陳述式。 因為結果集並非可捲動的如果應用程式存取的大型資料行值使用其中一種 get\<類型 > 的資料流的方法，驅動程式就會捨棄值只要在應用程式讀取它，就如同針對順向的唯讀狀態結果集。  
  
## <a name="see-also"></a>另請參閱  
 [善 JDBC Driver 的效能與可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
