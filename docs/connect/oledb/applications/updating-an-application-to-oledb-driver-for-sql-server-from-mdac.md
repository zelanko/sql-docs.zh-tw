---
title: OLE DB 驅動程式將應用程式更新 SQL server 的 MDAC |Microsoft 文件
description: 更新 MDAC 從 SQL Server 的 OLE DB 驅動程式的應用程式
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, vs. MDAC
- OLE DB Driver for SQL Server, vs. MDAC
- data access [OLE DB Driver for SQL Server], vs. MDAC
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 11597ed3b7cd80cae8604291bd8b662bf6a9ed80
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612103"
---
# <a name="updating-an-application-to-ole-db-driver-for-sql-server-from-mdac"></a>更新 MDAC 從 SQL Server 的 OLE DB 驅動程式的應用程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  有一些與 OLE DB 驅動程式的 SQL Server 和 Microsoft Data Access Components (MDAC); 之間的差異從 Windows Vista 開始，資料存取元件現在稱為 Windows Data Access Components （或 Windows DAC）。 雖然這兩者都提供原生資料存取[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫、 OLE DB 驅動程式的 SQL Server 已設計為可公開 （expose） 的新功能[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，而同時維護與舊版的回溯相容性。   

 此外，雖然 MDAC 包含元件使用 OLE DB、 ODBC 和 ActiveX Data Objects (ADO)、 OLE DB 驅動程式的 SQL Server 只會實作 OLE DB （雖然 ADO 可以存取 OLE DB 驅動程式的功能，適用於 SQL Server）。  

 OLE DB 驅動程式適用於 SQL Server 和 MDAC 差異在下列區域：  

-   使用 ADO 來存取 SQL Server 的 OLE DB 驅動程式的使用者可能會發現較少的篩選功能與存取 SQL OLE DB 提供者。  

-   如果 ADO 應用程式使用 SQL Server 的 OLE DB 驅動程式，而嘗試更新計算資料行，將會報告錯誤。 使用 MDAC 時，更新已接受，但會忽略。  

-   OLE DB 驅動程式的 SQL Server 是單一獨立的動態連結程式庫 (DLL) 檔案。 公開的介面已保留為最少量，這樣不但可便於散發，同時也可限制安全性風險。  

-   支援只 OLE DB 介面。  

-   SQL Server 名稱，OLE DB 驅動程式會與搭配 MDAC 使用的名稱不同。  

-   使用 SQL Server 的 OLE DB 驅動程式時，使用 MDAC 元件所提供的使用者可存取功能。 這包括但不限於以下項目：連接共用、ADO 支援和用戶端資料指標支援。 當使用這些功能時，OLE DB 驅動程式的 SQL Server 會提供只有資料庫連線。 MDAC 會提供類似追蹤、管理控制項和效能計數器的功能。  

-   應用程式可以使用 OLE DB 驅動程式與 OLE DB 核心服務的 SQL Server，但如果使用 OLE DB 資料指標引擎，它們應該使用的資料類型相容性選項，以避免可能發生因為資料指標引擎並不知道新的任何潛在問題[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]資料型別。  

-   OLE DB 驅動程式的 SQL Server 支援存取舊版[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫。  

-   OLE DB 驅動程式的 SQL Server 不包含 XML 整合。 OLE DB 驅動程式的 SQL Server 支援 SELECT... FOR XML 查詢，但不支援其他任何 XML 功能。 不過，支援 OLE DB 驅動程式的 SQL Server **xml**中導入的資料型別[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。  

-   OLE DB 驅動程式的 SQL Server 支援設定用戶端網路程式庫使用連接字串屬性。 如果您需要更完整的網路程式庫組態，您必須使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員。  

-   MDAC 連接字串允許的布林值 (**true**) 的**Trusted_Connection**關鍵字。 SQL Server 連接字串 OLE DB 驅動程式必須使用**是**或**沒有**。  

-   警告和錯誤發生了些微的變更。 警告和錯誤現在由伺服器傳回保留相同的嚴重性時傳遞至 OLE DB 驅動程式以供 SQL Server。 如果您依賴特定警告和錯誤的截獲，您應該確定您已經徹底測試過您的應用程式。  

-   OLE DB 驅動程式的 SQL Server 有更嚴格的錯誤檢查要比 MDAC，這表示，不符合嚴格的 OLE DB 規格的某些應用程式可能會有不同的行為。 例如，SQLOLEDB 提供者未強制執行規則的參數名稱開頭必須 ' @' 會針對結果參數，但 SQL Server OLE DB 驅動程式執行。  

-   OLE DB 驅動程式的 SQL Server 行為與 MDAC 不同有關連接失敗。 例如，MDAC 會傳回快取的屬性值之連接失敗，而 OLE DB 驅動程式的 SQL Server 報告的錯誤呼叫的應用程式。  

-   OLE DB 驅動程式的 SQL Server 不會產生 Visual Studio Analyzer 事件，而是產生 Windows 追蹤事件。  

-   OLE DB 驅動程式的 SQL Server 不能搭配 perfmon。 Perfmon 是一種 Windows 工具，它只能搭配使用 Windows 隨附之 MDAC SQLODBC 驅動程式的 DSN 一起使用。  

-   當 OLE DB 驅動程式的 SQL Server 連接至[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]和更新版本中，伺服器錯誤 16947 會以 SQL_ERROR 傳回。 當定點更新或刪除無法更新或刪除資料列時，就會發生這個錯誤。 使用 MDAC 時，如果連接到任何 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本，伺服器錯誤 16947 會以警告 (SQL_SUCCESS_WITH_INFO) 的形式傳回。  

-   OLE DB 驅動程式的 SQL Server 實作**IDBDataSourceAdmin**介面，這是選擇性的 OLE DB 介面，不是先前實作，但只限於**CreateDataSource**這個方法選擇性的介面實作。 [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

-   SQL Server OLE DB 驅動程式會傳回同義字中 TABLES 和 TABLE_INFO 結構描述資料列集，而且 TABLE_TYPE 會設定為同義字。  

-   傳回值的資料型別**varchar （max)**， **nvarchar （max)**， **varbinary （max)**， **xml**， **udt**，或其他大型物件類型不能傳回給用戶端版本早於[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 如果您想要使用這些類型當做傳回值，您必須使用適用於 SQL Server 的 OLE DB 驅動程式。  

-   MDAC 允許下列陳述式，執行手動和隱含交易的開頭但 OLE DB 驅動程式的 SQL Server 則不然。 它們必須在自動認可模式中執行。  

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

     此類型對應會影響資料行中繼資料傳回的值。 例如，**文字**資料行有大小上限為 2147483647，但是 OLE DB 驅動程式的 SQL Server 報告的大小上限**varchar （max)** 為 2,147,483,647 或-1，根據平台的資料行。  

-   OLE DB 驅動程式的 SQL Server 允許模稜兩可的連接字串 （例如，某些關鍵字可能會指定一次以上，和依據位置或優先順序解析可能會允許衝突的關鍵字） 回溯相容性的原因。 OLE DB 驅動程式的 SQL Server 的未來版本可能不允許模稜兩可的連接字串。 修改用來消除連接字串模稜兩可的相依性的 OLE DB 驅動程式的 SQL Server 的應用程式時，它會是很好的作法。  

-   如果您使用 OLE DB 呼叫來開始交易時，沒有 OLE DB 驅動程式的 SQL Server 和 MDAC; 之間的行為差異交易會立即開始使用 OLE DB 驅動程式的 SQL Server，但交易將會開始之後初次存取資料庫使用 MDAC。 這會影響預存程序和批次的行為，因為[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]需要@TRANCOUNT批次或預存程序完成執行時啟動批次或預存程序之後，必須相同。  

-   使用 OLE DB 驅動程式的 SQL Server，ITransactionLocal::BeginTransaction 會導致立即開始交易。 使用 MDAC 應用程式執行需要交易處於隱含交易模式的陳述式之前延遲交易的開始。 如需詳細資訊，請參閱 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md)。  


 SQL Server 和 MDAC 支援這兩個 OLE DB 驅動程式讀取認可的交易隔離資料列版本設定，但只有 OLE DB 驅動程式使用 SQL Server 支援快照集交易隔離。 (在程式設計的詞彙中，使用資料列版本設定的讀取認可交易隔離與讀取認可的交易相同)。  

## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
