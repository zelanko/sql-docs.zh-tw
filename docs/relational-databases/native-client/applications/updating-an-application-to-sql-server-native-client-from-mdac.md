---
title: 更新至 SQL Server Native Client 應用程式從 MDAC |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQLNCLI, vs. MDAC
- SQL Server Native Client, vs. MDAC
- data access [SQL Server Native Client], vs. MDAC
- SQL Server Native Client, updating applications
ms.assetid: 2860efdd-c59a-4deb-8a0e-5124a8f4e6dd
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 2065b627d9a3b9083451df6088dcb5944b436478
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39540698"
---
# <a name="updating-an-application-to-sql-server-native-client-from-mdac"></a>從 MDAC 將應用程式更新至 SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 與 Microsoft Data Access Components 之間有一些差異 (MDAC；從 Windows Vista 開始，資料存取元件現在稱為 Windows Data Access Components 或 Windows DAC)。 雖然兩者都提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的原生資料存取權，但是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 是專為公開 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的新功能而設計，同時還保留了與舊版的回溯相容性。  
  
 本主題的資訊可幫助您更新 MDAC (或 Windows DAC) 應用程式，使其保持為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中隨附的最新 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 版本。 為了讓此應用程式的版本保持[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]隨附的原生用戶端[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，請參閱[從 SQL Server 2005 Native Client 將應用程式更新](../../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md)。  
  
 此外，雖然 MDAC 包含了使用 OLE DB、ODBC 和 ActiveX Data Objects (ADO) 的元件，但是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 只會實作 OLE DB 和 ODBC (雖然 ADO 可以存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的功能)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 和 MDAC 還有下列其他方面的差異：  
  
-   使用 ADO 存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 提供者的使用者與存取 SQL OLE DB 提供者相較之下，可能會找到比較少的篩選功能。  
  
-   如果 ADO 應用程式使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 並嘗試更新計算資料行，將會報告錯誤。 在使用 MDAC 時，已接受更新但是被忽略。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 是單一獨立的動態連結程式庫 (DLL) 檔案。 公開的介面已保留為最少量，這樣不但可便於散發，同時也可限制安全性風險。  
  
-   只支援 OLE DB 和 ODBC 介面。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者和 ODBC 驅動程式的名稱與搭配 MDAC 使用的名稱不同。  
  
-   當使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 時，可以使用 MDAC 元件提供的使用者可存取功能。 這包括但不限於以下項目：連接共用、ADO 支援和用戶端資料指標支援。 當使用這些功能的任何一項時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 只會提供資料庫連接。 MDAC 會提供類似追蹤、管理控制項和效能計數器的功能。  
  
-   應用程式可以搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用 OLE DB 核心服務，但是如果使用 OLE DB 資料指標引擎，它們應該使用資料類型相容性選項來避免可能發生的任何問題，因為資料指標引擎並不知道新的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 資料類型。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 支援存取舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 不包含 XML 整合。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 支援 SELECT... FOR XML 查詢，但不支援其他類型的 XML 功能。 不過，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]支援原生用戶端**xml**中的資料類型導入[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 支援只利用連接字串屬性來設定用戶端網路程式庫。 如果您需要更完整的網路程式庫組態，您必須使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 與 odbcbcp.dll 不相容。 使用 ODBC 的應用程式和**bcp** Api 必須重建來連結 sqlncli11.lib，以便能夠使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端。  
  
-   Microsoft OLE DB provider for ODBC (MSDASQL) 不支援 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。 如果您要使用 MDAC SQLODBC 驅動程式搭配 MSDASQL 或使用 MDAC SQLODBC 驅動程式搭配 ADO，請在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中使用 OLE DB。  
  
-   MDAC 連接字串讓布林值 (**真**) 的**Trusted_Connection**關鍵字。 A[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端連接字串必須使用**yes**或是**沒有**。  
  
-   警告和錯誤發生了些微的變更。 伺服器傳回的警告和錯誤現在保持與傳遞給 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 時相同的嚴重性。 如果您依賴特定警告和錯誤的截獲，您應該確定您已經徹底測試過您的應用程式。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的錯誤檢查要比 MDAC 嚴格，這表示未嚴謹符合 ODBC 和 OLE DB 規格的某些應用程式可能會有不同的行為。 例如，SQLOLEDB 提供者未強制執行規則的參數名稱開頭必須 '\@' 結果的參數，但[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 對於失敗連接方面的行為與 MDAC 不同。 例如，MDAC 會針對失敗的連接傳回快取屬性值，而 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 會報告錯誤給呼叫的應用程式。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 不會產生 Visual Studio Analyzer 事件，而是產生 Windows 追蹤事件。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 不能搭配 Perfmon 一起使用。 Perfmon 是一種 Windows 工具，它只能搭配使用 Windows 隨附之 MDAC SQLODBC 驅動程式的 DSN 一起使用。  
  
-   當 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 連接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本時，伺服器錯誤 16947 會以 SQL_ERROR 的形式傳回。 當定點更新或刪除無法更新或刪除資料列時，就會發生這個錯誤。 使用 MDAC 時，如果連接到任何 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本，伺服器錯誤 16947 會以警告 (SQL_SUCCESS_WITH_INFO) 的形式傳回。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 會實作**IDBDataSourceAdmin**介面，這是選擇性的 OLE DB 介面，不是先前的實作，但只限於**CreateDataSource**的這個選擇性的方法介面的實作。 [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會在 TABLES 和 TABLE_INFO 結構描述資料列集中傳回同義字，而且 TABLE_TYPE 會設定為 SYNONYM。  
  
-   傳回值的資料型別**varchar （max)**， **nvarchar （max)**， **varbinary （max)**， **xml**， **udt**，或其他大型物件類型不會傳回至用戶端的版本早於[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 如果您想要使用這些類型當做傳回值，則必須使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。  
  
-   MDAC 允許在手動和隱含交易的開頭執行以下陳述式，但是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 則不允許。 它們必須在自動認可模式中執行。  
  
    -   所有全文檢索作業 (索引和目錄 DDL)  
  
    -   所有資料庫作業 (建立資料庫、改變資料庫、卸除資料庫)  
  
    -   重新設定  
  
    -   Shutdown  
  
    -   終止  
  
    -   Backup  
  
-   當 MDAC 應用程式連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中導入的資料類型將會以 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 相容的資料類型形式出現，如下表所示。  
  
    |SQL Server 2005 類型|SQL Server 2000 型別|  
    |--------------------------|--------------------------|  
    |**varchar(max)**|**text**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**image**|  
    |**udt**|**varbinary**|  
    |**xml**|**ntext**|  
  
     此類型對應會影響資料行中繼資料傳回的值。 例如，**文字**資料行有大小上限為 2,147,483,647，但[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 報告的最大大小**varchar （max)** SQL_SS_LENGTH_UNLIMITED，和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 報告的大小上限**varchar （max)** 為 2,147,483,647 或-1，根據平台的資料行。  
  
-   基於回溯相容性的理由，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 允許模稜兩可的連接字串 (例如，某些關鍵字可能會指定一次以上，而且可能會允許衝突的關鍵字，好讓解決方法以位置或優先順序為根據)。 未來的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 版本可能不允許模稜兩可的連接字串。 當修改應用程式，以便使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 來移除對於模稜兩可之連接字串的任何相依性時，這就是很好的作法。  
  
-   如果您使用 ODBC 或 OLE DB 呼叫來開始交易，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 與 MDAC 之間會有行為上的差異；使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 時會立即開始交易，但是使用 MDAC 時會在初次存取資料庫之後開始交易。 這會影響預存程序和批次的行為，因為[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]需要\@ \@TRANCOUNT 批次或預存程序完成執行時的批次或預存程序啟動之後必須相同。  
  
-   使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端，ITransactionLocal::BeginTransaction 會導致立即開始交易。 當使用 MDAC 時，交易會延遲到應用程式執行陳述式之後才開始，這需要交易處於隱含交易模式中。 如需詳細資訊，請參閱 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md)。  
  
-   使用時，您可能會遇到錯誤[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 驅動程式，以存取 System.Data.Odbc[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]會公開新的伺服器電腦[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-特定資料類型或功能。 System.Data.Odbc 提供一般的 ODBC 實作，而且後續不會公開供應商特有的功能或延伸模組。 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 驅動程式會更新為可原本就支援最新的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能)。若要解決此問題，您可以還原成 MDAC 或移轉至 System.Data.SqlClient。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 和 MDAC 都可使用資料列版本設定來支援讀取認可的交易隔離，但是只有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 可支援快照集交易隔離  (在程式設計的詞彙中，使用資料列版本設定的讀取認可交易隔離與讀取認可的交易相同)。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Native Client 建置應用程式](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
