---
title: 將應用程式從 MDAC 更新為適用於 SQL Server 的 OLE DB 驅動程式 | Microsoft Docs
description: 將應用程式從 MDAC 更新為適用於 SQL Server 的 OLE DB 驅動程式
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, vs. MDAC
- OLE DB Driver for SQL Server, vs. MDAC
- data access [OLE DB Driver for SQL Server], vs. MDAC
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 72f4406c4da07a1ddec422f09512dfe7cb28a028
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66778085"
---
# <a name="updating-an-application-to-ole-db-driver-for-sql-server-from-mdac"></a>將應用程式從 MDAC 更新為適用於 SQL Server 的 OLE DB 驅動程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  適用於 SQL Server 的 OLE DB 驅動程式與 Microsoft Data Access Components (MDAC) 之間有一些差異；從 Windows Vista 開始，資料存取元件現在稱為 Windows Data Access Components (或 Windows DAC)。 雖然兩者都提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的原生資料存取，但是適用於 SQL Server 的 OLE DB 驅動程式專為公開 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的新功能所設計，同時保留了與舊版之間的回溯相容性。   

 此外，雖然 MDAC 包含元件使用 OLE DB、 ODBC 和 ActiveX Data Objects (ADO)、 OLE DB Driver for SQL Server 只會實作 OLE DB （雖然 ADO 可以存取功能的 OLE DB Driver for SQL Server）。  

 OLE DB Driver for SQL Server 與 MDAC 不同，在下列區域：  

-   使用 ADO 存取 OLE DB Driver for SQL Server 的使用者可能會發現較少篩選的功能比存取 SQL OLE DB 提供者。  

-   如果 ADO 應用程式使用 OLE DB Driver for SQL Server，而嘗試更新計算資料行，就會報告錯誤。 使用 MDAC，系統會接受但忽略更新。  

-   OLE DB Driver for SQL Server 是單一獨立的動態連結程式庫 (DLL) 檔案。 公開的介面已保留為最少量，這樣不但可便於散發，同時也可限制安全性風險。  

-   支援只 OLE DB 介面。  

-   OLE DB Driver for SQL Server 名稱會與搭配 MDAC 使用的名稱不同。  

-   使用 OLE DB Driver for SQL Server 時，使用 MDAC 元件所提供的使用者可存取功能。 這包括但不限於以下項目：連接共用、ADO 支援和用戶端資料指標支援。 當使用任何一項功能時，OLE DB Driver for SQL Server 會提供僅資料庫連接。 MDAC 會提供類似追蹤、管理控制項和效能計數器的功能。  

-   應用程式可以搭配適用於 SQL Server 的 OLE DB 驅動程式使用 OLE DB 核心服務，但如果使用 OLE DB 資料指標引擎，則應使用資料類型相容性選項來避免可能發生的任何問題，原因是資料指標引擎並不知道新的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 資料類型。  

-   OLE DB Driver for SQL Server 支援存取舊版[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫。  

-   OLE DB Driver for SQL Server 不包含 XML 整合。 OLE DB Driver for SQL Server 支援 SELECT...FOR XML 查詢，但不支援其他類型的 XML 功能。 不過，支援 OLE DB Driver for SQL Server **xml**中的資料類型導入[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。  

-   適用於 SQL Server 的 OLE DB 驅動程式支援只利用連接字串屬性來設定用戶端網路程式庫。 如果您需要更完整的網路程式庫組態，您必須使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員。  

-   MDAC 連接字串讓布林值 (**真**) 的**Trusted_Connection**關鍵字。 OLE DB Driver for SQL Server 連接字串必須使用 **[是]** 或是**沒有**。  

-   警告和錯誤發生了些微的變更。 伺服器傳回的警告和錯誤在傳遞給適用於 SQL Server 的 OLE DB 驅動程式時，現在保持相同的嚴重性。 如果您依賴特定警告和錯誤的截獲，您應該確定您已經徹底測試過您的應用程式。  

-   適用於 SQL Server 的 OLE DB 驅動程式在錯誤檢查上比 MDAC 嚴格，這表示未嚴謹符合 OLE DB 規格的某些應用程式可能會有不同的行為。 例如，SQLOLEDB 提供者並未強制執行結果參數名稱的開頭必須是 '\@' 這項規則，但是適用於 SQL Server 的 OLE DB 驅動程式會強制執行這項規則。  

-   OLE DB Driver for SQL Server 行為與 MDAC 不同失敗的連線。 例如，MDAC 會針對失敗的連線傳回快取屬性值，而適用於 SQL Server 的 OLE DB 驅動程式則會報告錯誤給呼叫的應用程式。  

-   適用於 SQL Server 的 OLE DB 驅動程式不會產生 Visual Studio Analyzer 事件，而是產生 Windows 追蹤事件。  

-   OLE DB Driver for SQL Server 不能搭配 perfmon。 Perfmon 是一種 Windows 工具，它只能搭配使用 Windows 隨附之 MDAC SQLODBC 驅動程式的 DSN 一起使用。  

-   當 OLE DB Driver for SQL Server 連接到[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]和更新版本中，伺服器錯誤 16947 會以 SQL_ERROR 傳回。 當定點更新或刪除無法更新或刪除資料列時，就會發生這個錯誤。 使用 MDAC 時，如果連接到任何 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本，伺服器錯誤 16947 會以警告 (SQL_SUCCESS_WITH_INFO) 的形式傳回。  

-   適用於 SQL Server 的 OLE DB 驅動程式會實作 **IDBDataSourceAdmin** 介面，這是之前未實作的選擇性 OLE DB 介面，但是只會實作這個選擇性介面的 **CreateDataSource** 方法。 [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

-   適用於 SQL Server 的 OLE DB 驅動程式會在 TABLES 和 TABLE_INFO 結構描述資料列集中傳回同義字，並將 TABLE_TYPE 設定為 SYNONYM。  

-   資料類型 **varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 、**xml**、**udt** 或其他大型物件類型的傳回值無法傳回給 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以前的用戶端版本。 如果您想要使用這些類型當做傳回值，您必須使用 OLE DB Driver for SQL Server。  

-   MDAC 允許在手動和隱含交易的開頭執行下列陳述式，但適用於 SQL Server 的 OLE DB 驅動程式則不允許。 它們必須在自動認可模式中執行。  

    -   所有全文檢索作業 (索引和目錄 DDL)  

    -   所有資料庫作業 (建立資料庫、改變資料庫、卸除資料庫)  

    -   重新設定  

    -   Shutdown  

    -   終止  

    -   Backup  

-   當 MDAC 應用程式連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中導入的資料類型將會以 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 相容的資料類型形式出現，如下表所示。  

    |SQL Server 2005 類型|SQL Server 2005 類型|  
    |--------------------------|--------------------------|  
    |**varchar(max)**|**text**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**image**|  
    |**udt**|**varbinary**|  
    |**xml**|**ntext**|  

     此類型對應會影響資料行中繼資料傳回的值。 例如，**文字**資料行的最大大小為 2147483647，但是 OLE DB Driver for SQL Server 報告的大小上限**varchar （max)** 為 2,147,483,647 或-1，根據平台的資料行。  

-   基於回溯相容性的理由，適用於 SQL Server 的 OLE DB 驅動程式允許模稜兩可的連接字串 (例如，可多次指定某些關鍵字，而且可允許衝突的關鍵字，解決方法是以位置或優先順序為根據)。 OLE DB Driver for SQL Server 的未來版本可能不允許模稜兩可的連接字串。 修改應用程式時，適合使用適用於 SQL Server 的 OLE DB 驅動程式來消除任何對於模稜兩可連接字串的相依性。  

-   如果您使用的 OLE DB 呼叫來開始交易時，沒有 OLE DB Driver for SQL Server 和 MDAC; 之間的行為差異交易會立即開始利用 OLE DB Driver for SQL Server，但交易將會開始之後的第一個資料庫可讓您存取使用 MDAC。 這會影響預存程序和批次的行為，原因是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 要求 @@TRANCOUNT 在批次或預存程序完成執行的前後必須相同。  

-   OLE DB Driver for SQL Server，ITransactionLocal::BeginTransaction 會立即開始交易。 當使用 MDAC 時，交易會延遲到應用程式執行需要在隱含交易模式中之交易的陳述式之後才開始。 如需詳細資訊，請參閱 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md)。  


 這兩個 OLE DB Driver for SQL Server 和 MDAC 支援讀取認可的交易隔離使用資料列版本設定，但只有 OLE DB Driver for SQL Server 支援快照集交易隔離。 (在程式設計的詞彙中，使用資料列版本設定的讀取認可交易隔離與讀取認可的交易相同)。  

## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
