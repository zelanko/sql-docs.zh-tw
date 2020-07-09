---
title: MSSQLSERVER_824 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 824 (Database Engine error)
ms.assetid: 2aa22246-2712-4fdb-9744-36e7e6f3175e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f33df8f287cc60c34035ee22b8a03be65440f6ee
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767850"
---
# <a name="mssqlserver_824"></a>MSSQLSERVER_824
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|824|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|B_HARDSSERR|  
|訊息文字|SQL Server 偵測到邏輯的一致性 I/O 錯誤: %ls。 這是當在檔案 '%ls' 中位移 %#016I64x 的資料庫識別碼 %d 之頁面 %S_PGID 進行 %S_MSG 的期間所發生的。  SQL Server 錯誤記錄檔和系統事件記錄檔中的訊息，或許可以提供其他詳細資訊。|  
  
## <a name="symptom"></a>徵狀  


如果在讀取或寫入資料庫頁面之後發生邏輯一致性檢查失敗，您可能會在 SQL Server 錯誤記錄檔或 Windows 應用程式事件記錄檔中看到下列錯誤訊息：
 
``` 
2009-11-02 15:46:42.90 spid51      Error: 824, Severity: 24, State: 2.
2009-11-02 15:46:42.90 spid51      SQL Server detected a logical consistency-based I/O error: incorrect pageid (expected 1:43686; actual 0:0). It occurred during a read of page (1:43686) in database ID 23 at offset 0x0000001554c000 in file 'H:\MSSQL.SQL2008\MSSQL\DATA\my_db.mdf'.  Additional messages in the SQL Server error log or system event log may provide more detail. This is a severe error condition that threatens database integrity and must be corrected immediately. Complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.
```
 
如果應用程式在查詢或修改資料時出現此訊息，則會將錯誤訊息傳回至應用程式，並終止資料庫連接。 
  
## <a name="cause"></a>原因
此錯誤表示 Windows 回報從磁碟成功讀取頁面，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發現頁面錯誤。 此錯誤與錯誤 823 類似，不同的是 Windows 並未偵測到此錯誤，且通常表示 I/O 子系統發生問題，例如磁碟機故障、磁碟韌體問題、錯誤的裝置驅動程式等。 如需 I/O 錯誤的詳細資訊，請參閱[Microsoft SQL Server I/O Basics, Chapter 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10)) (第 2 章 Microsoft SQL Server I/O 基本概念)。  

SQL Server 使用 Windows API (例如 ReadFile、WriteFile、ReadFileScatter、WriteFileGather) 來執行 I/O 作業。 執行這些 I/O 作業之後，SQL Server 會檢查是否有與這些 API 呼叫建立關聯的錯誤狀況。 如果這些 API 呼叫因作業系統錯誤而失敗，則 SQL Server 會報告錯誤823。 在某些情況下，Windows API 呼叫實際上會成功，但 I/O 作業所傳輸的資料可能發生了邏輯一致性問題。 這些邏輯一致性問題是透過錯誤 824 回報。
 
此 824 錯誤包含下列資訊：

- I/O 作業執行對象的資料庫檔案
- 嘗試執行 I/O 作業的檔案位移
- 這個檔案所屬的資料庫
- 與 I/O 作業相關的頁碼
- 作業是讀取或寫入作業
- 失敗的邏輯一致性檢查相關詳細資料 [檢查類型、用於這項檢查的實際值和預期值]
 
這些邏輯一致性檢查是由 SQL Server 執行的額外完整性檢查，以確保在整個 I/O 作業期間維護涉及資料傳輸的資料特定重要層面。 這些檢查包括總和檢查碼、損毀頁、短傳輸、錯誤頁面識別碼、過時讀取、頁面稽核失敗。 所執行檢查其本質會根據資料庫和伺服器層級的不同組態選項而有所不同。 
 
824 錯誤訊息通常表示基礎儲存系統或硬體或 I/O 要求路徑中的磁碟機發生問題。 當檔案系統中出現不一致，或資料庫檔案損毀時，就可能會遇到這個錯誤。

## <a name="resolution"></a>解決方案  

如果發生錯誤 824，可嘗試下列解決方法： 

- 檢閱 msdb 中的 [suspect_pages](../backup-restore/manage-the-suspect-pages-table-sql-server.md) 資料表，以查看是否有其他頁面 [在相同或不同的資料庫中] 發生此問題。
- 使用 DBCC CHECKDB 命令來檢查 [與 824 訊息所報告的] 相同磁碟區的資料庫是否一致。 如果 DBCC CHECKDB 命令找出不一致，則請使用知識庫文章[如何針對 DBCC CHECKDB 報告的資料庫一致性錯誤進行疑難排解](https://support.microsoft.com/help/2015748/how-to-troubleshoot-database-consistency-errors-reported-by-dbcc-check) (機器翻譯) 中的指引。
- 如果發生這些 824 錯誤的資料庫未開啟 PAGE_VERIFY CHECKSUM 資料庫選項，請立即執行此動作。 824 錯誤可能有總和檢查碼失敗以外的其他發生原因，但 CHECKSUM 是將頁面寫入磁碟之後驗證頁面一致性的最佳選擇。
- 檢查 Windows 事件記錄檔中是否有從作業系統或儲存裝置或裝置驅動程式回報的任何錯誤或訊息。 如其在某方面與此錯誤相關，請先解決這些錯誤。 例如，除 824 訊息以外，您可能也會注意到事件記錄檔中由磁碟來源回報的「驅動程式在 \Device\Harddisk4\DR4 上偵測到控制器錯誤」之類事件。 在此情況下，您必須評估此檔案是否存在於此裝置上，然後先更正這些磁碟錯誤。
- 使用 [SQLIOSim](https://support.microsoft.com/help/231619/how-to-use-the-sqliosim-utility-to-simulate-sql-server-activity-on-a-d) 公用程式，找出這些 824 錯誤能否在一般 SQL Server I/O 要求外重現。 SQLIOSim 隨附於 SQL Server 2008，因此不需要在此版本或更新版本上另行下載。
- 請與硬體廠商或裝置製造商合作，以確保：
   - 硬體裝置和組態符合 [SQL Server 的 I/O 需求](https://support.microsoft.com/help/967576/microsoft-sql-server-database-engine-input-output-requirements) (英文)。
   - I/O 路徑中所有裝置的裝置驅動程式和其他支援軟體元件都已更新。
- 如果硬體廠商或裝置製造商提供了任何診斷公用程式，則請使用這些程式來評估 I/O 系統的健全狀況。
- 評估存在於這些 I/O 要求路徑中的篩選器驅動程式是否發生問題。
   - 檢查這些篩選器驅動程式是否有任何更新
   - 可否移除或停用這些篩選器驅動程式，以觀察導致 824 錯誤的問題是否消失
- 如果問題與硬體無關，而且確定有未受影響的備份可以使用，請利用該備份來還原資料庫。  

## <a name="see-also"></a>另請參閱  
[管理 suspect_pages 資料表 &#40;SQL Server&#41;](~/relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
