---
title: 儲存追蹤及追蹤範本 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- exporting trace templates
- importing trace templates
- SQL Server Profiler, templates
ms.assetid: 957e6bf8-e7a3-4a59-a1cd-0a41538a8158
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf12d70f78a18b24b7fd6638d788d4e5b436c21c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47653400"
---
# <a name="save-traces-and-trace-templates"></a>儲存追蹤及追蹤範本
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  區分儲存追蹤檔案與儲存追蹤範本是很重要的。 儲存追蹤檔案牽涉到將擷取的事件資料儲存到指定的位置上。 儲存追蹤範本則牽涉到儲存追蹤的定義，例如指定的資料行、事件類別或篩選等。  
  
## <a name="saving-traces"></a>儲存追蹤  
 若您必須於稍後分析或重新執行擷取的資料，請將擷取的事件資料儲存到檔案或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中。 使用追蹤檔案可執行下列作業：  
  
-   使用追蹤檔案或追蹤資料表來建立工作負載，以作為 Database Engine Tuning Advisor 的輸入項目。  
  
-   使用追蹤檔可以擷取事件，並將追蹤檔傳給支援提供者以進行分析。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的查詢處理工具以存取資料，或檢視 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]中的資料。 只有 **系統管理員** 固定伺服器角色的成員或資料表建立者，才能直接存取追蹤資料表。  
  
> [!NOTE]  
>  將追蹤資料擷取到資料表，比擷取到檔案還慢。 替代方式是將追蹤資料擷取到檔案中，開啟追蹤檔案，然後再將追蹤另存成追蹤資料表。  
  
 使用追蹤檔案時， [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 會將擷取的事件資料 (不是追蹤定義) 儲存到 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] Trace (\*.trc) 檔案中。 儲存追蹤檔案時副檔名會自動加到檔案結尾，而不論其他指定的副檔名為何。 例如，若您指定名為 **Trace.dat**的追蹤檔案時，建立的檔案便稱為 **Trace.dat.trc**。  
  
> [!IMPORTANT]  
>  具有 SHOWPLAN、ALTER TRACE 或 VIEW SERVER STATE 權限的使用者可以檢視執行程序表輸出中所擷取的查詢。 這些查詢可能會包含類似密碼的敏感資訊。 因此，我們建議您只能將這些權限授與給有權檢視敏感資訊的使用者，例如 **db_owner** 固定資料庫角色的成員或是 **系統管理員** 固定伺服器角色的成員。 此外，我們也建議您只將執行程序表檔案或是包含與執行程序表相關之事件的追蹤檔案儲存到使用 NTFS 檔案系統的位置，並建議您將存取權限制為有權檢視敏感資訊的使用者。  
  
## <a name="saving-templates"></a>儲存範本  
 追蹤的範本定義包含事件類別、資料行、篩選和用於建立追蹤的所有其他屬性 (擷取的事件資料除外)。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 針對一般追蹤工作和特定工作，例如建立可供 Database Engine Tuning Advisor 用來微調實體資料庫設計的工作負載，提供了預先定義的系統範本。 您也可以建立與儲存使用者自訂的範本。  
  
### <a name="importing-and-exporting-templates"></a>匯入和匯出範本  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 可讓您在不同的伺服器之間匯入和匯出範本。 匯出範本時，會將現有範本的副本移至您所指定的目錄中。 匯入範本時，則會複製您所指定的範本。 在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]中檢視這些範本時，您可以藉由範本名稱後的 "(user)" 這個詞彙來與系統範本作區別。 您無法覆寫或直接修改預先定義的系統範本。  
  
### <a name="analyzing-performance-with-templates"></a>以範本分析效能  
 若您經常監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請使用範本來分析效能。 範本每次都會擷取相同的事件資料，並使用相同的追蹤定義來監視相同的事件。 您不需在每次建立追蹤時都定義事件類別與資料行。 此外，範本可以提供給另一位使用者，用來監視特定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件。 例如，支援提供者可以為使用者提供範本。 客戶可使用範本來擷取所需的事件資料，再將事件資料傳送給支援提供者以進行分析。  
  
 **若要將追蹤儲存至檔案**  
  
 [將追蹤結果儲存至檔案 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)  
  
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [將追蹤結果儲存到資料表 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)   
 [建立追蹤範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)   
 [從執行中的追蹤衍生範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [從追蹤檔案或追蹤資料表衍生範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [匯出追蹤範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)   
 [匯入追蹤範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
  
