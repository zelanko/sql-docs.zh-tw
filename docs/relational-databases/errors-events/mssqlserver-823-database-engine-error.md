---
title: MSSQLSERVER error 823  | mssqlserver_823
description: Microsoft SQL Server 錯誤 823 (mssqlserver_823) 的描述和一些常用解決方案，這是很嚴重的系統層級錯誤情況，其會威脅到資料庫的完整性，必須立即處理。
ms.custom: ''
ms.date: 01/27/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 823 (Database Engine error)
ms.assetid: 0d9fce3c-3772-46ce-a7a3-4f4988dc6cae
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 57850e8b54ef0f99895e558616b22089af266895
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767852"
---
# <a name="mssqlserver-error-823"></a>MSSQLSERVER 錯誤 823
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|823|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|B_HARDERR|  
|訊息文字|作業系統將錯誤 %ls 傳回給 SQL Server，期間：%S_MSG 在 %#016I64x 位移，檔案：'%ls'。 SQL Server 錯誤記錄檔和系統事件記錄檔中的訊息或許可以提供其他詳細資訊。 這是嚴重的系統層級錯誤狀況，且可能會損及資料庫的完整性，所以必須立即更正。 請執行完整的資料庫一致性檢查 (DBCC CHECKDB)。 導致這個錯誤的原因有許多可能性; 如需詳細資訊，請參閱《SQL Server 線上叢書》。|  
  
## <a name="explanation"></a>說明  
SQL Server 使用 Windows API (例如，[ReadFile](/windows/win32/api/fileapi/nf-fileapi-readfile)、[WriteFile](/windows/win32/api/fileapi/nf-fileapi-writefile)、[ReadFileScatter](/windows/win32/api/fileapi/nf-fileapi-readfilescatter)、[WriteFileGather](/windows/win32/api/fileapi/nf-fileapi-writefilegather)) 來執行檔案 I/O 作業。 執行這些 I/O 作業之後，SQL Server 會檢查是否有與這些 API 呼叫建立關聯的錯誤狀況。 如果 API 呼叫因作業系統錯誤而失敗，則 SQL Server 會報告錯誤823。

 823 錯誤訊息包含下列資訊：
 - I/O 作業執行對象的資料庫檔案
 - 嘗試執行 I/O 作業的檔案中位移位置。 這是檔案開頭的實體位元組位移。 將此數字除以 8192，就會得出受到錯誤影響的邏輯頁碼。
 - I/O 作業是讀取還是寫入要求
 - 括弧中的作業系統錯誤代碼和錯誤描述
 

**作業系統錯誤：** 讀取或寫入 Windows API 呼叫不成功，且 SQL Server 發生與 Windows API 呼叫相關的作業系統錯誤。 下列為 823 錯誤訊息範例：

```
Error: 823, Severity: 24, State: 2.
2010-03-06 22:41:19.55 spid58 The operating system returned error 1117 (The request could not be performed because of an I/O device error.) to SQL Server during a read at offset 0x0000002d460000 in file 'e:\program files\Microsoft SQL Server\mssql\data\mydb.MDF'. Additional messages in the SQL Server error log and system event log may provide more detail. This is a severe, system-level error condition that threatens database integrity and must be corrected immediately. It is recommended to complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.
```

在與錯誤訊息中的檔案建立關聯的資料庫上，您不一定會看到 DBCC CHECKDB 陳述式中的錯誤。 當您看到 823 錯誤時，可以執行 DBCC CHECKDB 陳述式。 如果 DBCC CHECKDB 陳述式未報告任何錯誤，則可能發生了間歇性的系統問題或磁碟問題。

當您使用追踪旗標 818 時，可能會將 823 錯誤的其他診斷資訊寫入 SQL Server 錯誤記錄檔。
如需詳細資訊，請參閱 [KB 826433：新增額外的 SQL Server 診斷，以偵測未報告的 I/O 問題](https://support.microsoft.com/help/826433/sql-server-diagnostics-added-to-detect-unreported-i-o-problems-due-to)


## <a name="cause"></a>原因
823 錯誤訊息通常表示基礎儲存系統或硬體或 I/O 要求路徑中的磁碟機發生問題。 當檔案系統中出現不一致，或資料庫檔案損毀時，就可能會遇到這個錯誤。 如已讀取檔案，則 SQL Server 在傳回 823 之前已重試四次讀取要求。 如果重試作業成功，則查詢不會失敗，但訊息 [825](mssqlserver-825-database-engine-error.md) 會寫入錯誤記錄和事件記錄檔。

## <a name="user-action"></a>使用者動作  
 - 檢閱 MSDB 中的 [suspect_pages](../system-tables/suspect-pages-transact-sql.md) 資料表，是否有其他頁面發生此問題 (相同的資料庫或不同的資料庫)。
 - 使用 DBCC CHECKDB 命令來檢查 (與 823 訊息所報告的) 相同磁碟區的資料庫是否一致。 如果 DBCC CHECKDB 命令找出不一致，則請使用[如何疑難排解 DBCC CHECKB 報告的資料庫一致性錯誤](https://support.microsoft.com/help/2015748/how-to-troubleshoot-database-consistency-errors-reported-by-dbcc-check)中的指引。 
 - 檢查 Windows 事件記錄檔中是否有從作業系統或儲存裝置或裝置驅動程式回報的任何錯誤或訊息。 如其在某方面與此錯誤相關，請先解決這些錯誤。 例如，除 823 訊息以外，您可能也會注意到事件記錄檔中由磁碟來源回報的「驅動程式在 \Device\Harddisk4\DR4 上偵測到控制器錯誤」之類事件。 在此情況下，您必須評估此檔案是否存在於此裝置上，然後先更正這些磁碟錯誤。
 - 使用 [SQLIOSim](https://support.microsoft.com/help/231619/how-to-use-the-sqliosim-utility-to-simulate-sql-server-activity-on-a-d) 公用程式，找出這些 823 錯誤能否在一般 SQL Server I/O 要求外重現。 SQLIOSim 公用程式隨附於 SQL Server 2008 和更新版本，因此不需要另行下載。 其通常位在 `C:\Program Files\Microsoft SQL Server\MSSQLxx.MSSQLSERVER\MSSQL\Binn` 資料夾中。
 - 請與您的硬體廠商或裝置製造商合作，以確保
   - 硬體裝置和設定符合 SQL Server 的 I/O 需求
   - I/O 路徑中所有裝置的裝置驅動程式和其他支援軟體元件均為最新
 - 如果硬體廠商或裝置製造商向您提供了任何診斷公用程式，則請使用這些程式來評估 I/O 系統的健康狀態
 - 評估存在於這些 I/O 要求路徑中的[篩選器驅動程式](https://support.microsoft.com/help/2454053/use-of-system-filter-drivers-can-lead-to-sql-server-database-engine-pe)是否發生問題。
   - 檢查這些篩選器驅動程式是否有任何更新
   - 可否移除或停用這些篩選器驅動程式，以觀察導致 823 錯誤的問題是否消失  
