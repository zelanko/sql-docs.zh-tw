---
title: XEvents 概觀 - SQL Server
description: SQL Server 擴充事件架構可供收集識別效能問題並對其進行疑難排解所需的資料。 該架構為可設定且可調整的。
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: overview
helpviewer_keywords:
- extended events [SQL Server]
- xe
- XEvents
ms.assetid: bf3b98a6-51ed-4f2d-9c26-92f07f1fa947
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c837902edb7baa43d7fa07cfefc8ec335dc4183e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465529"
---
# <a name="extended-events-overview"></a>擴充事件概觀

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]「擴充事件」架構可讓使用者收集進行疑難排解或識別效能問題所需的資料 (盡可能多或少)。 擴充事件是可設定的，而且它會非常妥善地調整。

您可以在下列位置找到「擴充事件」的詳細資訊：[快速入門：SQL Server 中的延伸事件](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)。

## <a name="benefits-of-ssnoversion-extended-events"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 擴充事件的優點  

「擴充事件」是一種使用小量效能資源的一種輕量型效能監視系統。 擴充事件提供兩個圖形化使用者介面，用以建立、修改、顯示及分析您的工作階段資料。 這些介面的名稱如下：

- 新增工作階段精靈
- 新增工作階段

## <a name="extended-events-concepts"></a>擴充事件概念  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]「擴充事件」是以現有概念 (例如，事件或事件取用者) 為建置基礎、使用 Windows 事件追蹤的概念，並引進新的概念。  
  
 下表描述擴充事件的概念。  
  
|主題|描述|  
|-----------|-----------------|  
|[SQL Server 擴充的事件套件](../../relational-databases/extended-events/sql-server-extended-events-packages.md)|描述包含物件的「擴充事件」套件。 當「擴充事件」工作階段在執行時，系統會使用這些物件來取得和處理資料。|  
|[SQL Server 擴充的事件目標](/previous-versions/sql/sql-server-2016/bb630339(v=sql.130))|描述事件工作階段期間可以接收資料的事件取用者。|  
|[SQL Server 擴充的事件引擎](../../relational-databases/extended-events/sql-server-extended-events-engine.md)|描述可實作和管理擴充事件工作階段的引擎。|  
|[SQL Server 擴充的事件工作階段](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)|描述擴充事件工作階段。|  
| &nbsp; | &nbsp; |
  
## <a name="extended-events-architecture"></a>擴充事件架構  

「擴充事件」是我們對用於伺服器系統的一般事件處理系統的稱呼。 擴充的事件基礎結構可支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中資料的相互關聯，而在某些條件下，則可支援作業系統和資料庫應用程式中資料的相互關聯。 在作業系統案例中，「擴充事件」輸出必須導向 Windows 事件追蹤 (ETW)。 ETW 可將事件資料與作業系統或應用程式事件資料相互關聯。  

所有應用程式都有執行點，這些執行點在應用程式內部和外部都很實用。 在應用程式內，可以使用工作最初執行期間所收集的資訊將非同步處理加入佇列。 在應用程式外，執行點會提供資訊給監視公用程式。 該資訊是關於受監視應用程式的行為和效能特性。  

 擴充的事件可支援在處理序外使用事件資料。 這些資料通常是由以下項目所使用：  
  
-   追蹤工具，例如 SQL 追蹤和系統監視器。  
  
-   記錄工具，例如 Windows 事件記錄檔或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔。  
  
-   管理產品或是開發產品上之應用程式的使用者。  
  
 「擴充事件」具有下列重要的設計層面：  
  
-   「擴充事件」引擎無法得知事件。 此引擎可將任何事件繫結至任何目標，因為此引擎不受到事件內容限制。 如需有關擴充的事件引擎的詳細資訊，請參閱＜ [SQL Server Extended Events Engine](../../relational-databases/extended-events/sql-server-extended-events-engine.md)＞。  
  
-   事件會與事件取用者區隔，後者在擴充的事件中稱為 *「目標」* 。 這表示，任何目標都可以接收任何事件。 此外，目標可以自動耗用任何引發的事件，這樣可以記錄或提供其他事件內容。 如需詳細資訊，請參閱＜ [SQL Server Extended Events Targets](/previous-versions/sql/sql-server-2016/bb630339(v=sql.130))＞。  
  
-   事件與事件發生時所要採取的動作不同。 因此，任何動作都可以與任何事件產生關聯。  
  
-   述詞可以動態篩選何時應該擷取事件資料。 動態篩選會增加「擴充事件」基礎結構的彈性。 如需詳細資訊，請參閱＜ [SQL Server Extended Events Packages](../../relational-databases/extended-events/sql-server-extended-events-packages.md)＞。  
  
 擴充的事件可以同步產生事件資料 (以及非同步處理該資料)，這樣可為事件處理提供彈性的方案。 此外，擴充的事件還提供下列功能：  
  
-   在伺服器系統上處理事件的統一方式，同時也可讓使用者隔離特定的事件來進行疑難排解。  
  
-   與現有的 ETW 工具整合並支援這些工具。  
  
-   可根據 [!INCLUDE[tsql](../../includes/tsql-md.md)]完整設定的事件處理機制。  
  
-   能夠動態監視使用中處理序，同時對這些處理序有最少的影響。  
  
-   執行的預設系統健康工作階段，而不會有任何顯著的效能影響。 此工作階段會收集系統資料，讓您能夠用來協助排除效能問題。 如需詳細資訊，請參閱 [使用 system_health 工作階段](../../relational-databases/extended-events/use-the-system-health-session.md)。  
  
## <a name="extended-events-tasks"></a>擴充事件工作  

使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料定義語言 (DDL) 陳述式、動態管理檢視和函數或目錄檢視時，您可以針對您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境建立簡單或複雜 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 「擴充事件」疑難排解方案。  
  
|工作描述|主題|  
|----------------------|-----------|  
|使用 **[物件總管]** 管理事件工作階段。|[在物件總管中管理事件工作階段](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md)|  
|描述如何建立擴充事件工作階段。|[建立擴充事件工作階段](/previous-versions/sql/sql-server-2016/hh213147(v=sql.130))|  
|描述如何檢視及重新整理目標資料。| [進階檢視 SQL Server 中擴充事件的目標資料](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)|  
|描述如何使用擴充事件工具來建立和管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 「擴充事件」工作階段。|[擴充事件工具](../../relational-databases/extended-events/extended-events-tools.md)|  
|描述如何改變擴充事件工作階段。|[更改擴充事件工作階段](../../relational-databases/extended-events/alter-an-extended-events-session.md)|  
|描述如何取得與事件有關之欄位的資訊。|[取得所有事件的欄位](/previous-versions/sql/sql-server-2016/bb677249(v=sql.130))|  
|描述如何在註冊的封裝中查明哪些事件可用。|[檢視已註冊之套件的事件](./selects-and-joins-from-system-views-for-extended-events-in-sql-server.md)|  
|描述如何判斷哪些擴充事件目標可在註冊的封裝中使用。|[檢視已註冊之套件的擴充事件目標](/previous-versions/sql/sql-server-2016/bb677247(v=sql.130))|  
|描述如何檢視同等於每一個 SQL 追蹤事件及其關聯資料行的「擴充事件」事件和動作。|[檢視同等於 SQL 追蹤事件類別的擴充事件](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)|  
|描述當您在 CREATE EVENT SESSION 或 ALTER EVENT SESSION 中使用 ADD TARGET 引數時，如何尋找可以設定的參數。|[取得 ADD TARGET 引數的可設定參數](/previous-versions/sql/sql-server-2016/bb677176(v=sql.130))|  
|描述如何將現有的 SQL 追蹤指令碼轉換為擴充事件工作階段。|[將現有的 SQL 追蹤指令碼轉換為擴充事件工作階段](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md)|  
|描述如何判斷哪些查詢持有鎖定、查詢的計畫，以及取得鎖定時的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 堆疊。|[判斷哪些查詢持有鎖定](../../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)|  
|描述如何識別阻礙資料庫效能的鎖定來源。|[尋找持有最多鎖定的物件](../../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)|  
|描述如何搭配 Windows 事件追蹤來使用擴充事件，以監視系統活動。|[使用擴充事件監視系統活動](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)|  
|使用擴充事件的目錄檢視和動態管理檢視 (DMV) | [SQL Server 擴充事件系統檢視表中的 SELECT 和 JOIN](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md) |
| &nbsp; | &nbsp; |

使用下列 Transact-SQL (T-SQL) 查詢來列出所有可能的擴充事件及其描述：

```sql
SELECT
     obj1.name as [XEvent-name],
     col2.name as [XEvent-column],
     obj1.description as [Descr-name],
     col2.description as [Descr-column]
  FROM
               sys.dm_xe_objects        as obj1
      JOIN sys.dm_xe_object_columns as col2 on col2.object_name = obj1.name
  ORDER BY
    obj1.name,
    col2.name
```


## <a name="code-examples-can-differ-for-azure-sql-database"></a>適用於 Azure SQL Database 的程式碼範例可能有所不同

[!INCLUDE[sql-on-premises-vs-azure-similar-sys-views-include.](../../includes/paragraph-content/sql-on-premises-vs-azure-similar-sys-views-include.md)]

## <a name="see-also"></a>另請參閱

[資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)  
[SQL Server 物件與版本的 DAC 支援](/previous-versions/sql/sql-server-2012/ee210549(v=sql.110))  
[部署資料層應用程式](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)  
[監視資料層應用程式](../../relational-databases/data-tier-applications/monitor-data-tier-applications.md)  
&nbsp;  
[擴充事件動態管理檢視](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)  
[擴充事件目錄檢視 (Transact-SQL)](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)  
&nbsp;  
[XELite：跨平台程式庫，用來讀取 XEL 檔案或即時 SQL 串流中的 XEvent](https://www.nuget.org/packages/Microsoft.SqlServer.XEvent.XELite/)，於 2019 年 5 月發行。  
[Read-SQLXEvent PowerShell Cmdlet](https://www.powershellgallery.com/packages/SqlServer.XEvent)，發行日期 2019 年 6 月。  
[SQL 謎團：XEvent 工作階段的原因追蹤與事件順序 (2019 年 4 月 1 日發佈於部落格)](https://bobsql.com/sql-mysteries-causality-tracking-vs-event-sequence-for-xevent-sessions/) \(英文\)