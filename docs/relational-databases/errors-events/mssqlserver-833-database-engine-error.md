---
title: MSSQLSERVER_833 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 833 (Database Engine error)
ms.assetid: 14129cc4-be80-4772-9e3f-0e5da4d0696b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3f58165bd38e281b6c0223ae11c20a76f1bcdd5b
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435537"
---
# <a name="mssqlserver_833"></a>MSSQLSERVER_833
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|833|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|BUF_LONG_IO|  
|訊息文字|SQL Server 在資料庫 `[%ls] (%d)` 中的檔案 [%ls] 上發現 %d 次花費 %d 秒以上才完成的 I/O 要求。  作業系統檔案控制代碼為 0x%p。  最新的長 I/O 的位移為: %#016I64x。|  
  
## <a name="explanation"></a>說明  
此訊息表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已經從磁碟發出讀取或寫入要求，且該要求花費超過 15 秒才傳回。 此錯誤是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 回報，並且表示 I/O 子系統發生問題。 您可能也會注意到與此訊息相關聯的其他徵兆：PAGEIOLATCH 等候的延遲時間很長、系統事件記錄檔中的警告或錯誤、系統監視器計數器中的磁碟延遲問題指示。 
  
### <a name="possible-causes"></a>可能的原因  
造成此問題的原因可能是作業系統效能問題、硬體錯誤、韌體錯誤、裝置驅動程式問題，或篩選驅動程式介入 I/O 處理序或資料庫檔案的儲存體路徑。 SQL Server 會記錄其起始 I/O 要求的時間，並記錄 I/O 完成的時間。 如果該差異為 15 秒或更久，則會偵測到此狀況。 這也表示，SQL Server 不是此訊息所描述及報告延遲 I/O 狀況的原因。 這種情況通常稱為「停止 I/O」。 大部分的磁碟要求都是在磁碟的一般速度內進行。 這個典型的磁碟速度通常稱為「磁碟搜尋時間」。 大多數標準磁碟的磁碟搜尋時間會在 10 毫秒內 (或更少) 發生。 因此，對於系統 I/O 路徑回到 SQL Server 來說，15 秒是很長的時間。 
  
## <a name="user-action"></a>使用者動作  
查看系統事件記錄檔中是否有與硬體相關的錯誤訊息，以便對此錯誤進行疑難排解。 同時，也查看硬體特定的記錄檔 (如果有的話)。 您應該使用必要方法和技術來判斷造成作業系統延遲的原因 (透過驅動程式或透過 I/O 硬體)。 此問題的解決方法可能牽涉到更新所有裝置驅動程式和韌體，或執行與您磁碟系統相關聯的其他診斷。 
  
使用「效能監視器」檢查下列計數器︰  
  
-   **Average Disk Sec/Transfer**  
  
-   **Average Disk Queue Length**  
  
-   **Current Disk Queue Length**  
  
例如，在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦上，**Average Disk Sec/Transfer** 時間通常少於 15 毫秒。 如果 **Average Disk Sec/Transfer** 值增加，表示 I/O 子系統並未以最佳的方式應付 I/O 需要。

您也可以使用像是 [Storport ETW 記錄](https://docs.microsoft.com/archive/blogs/ntdebugging/storport-etw-logging-to-measure-requests-made-to-a-disk-unit) \(英文\) 的設備來測量對磁碟單位提出的要求延遲。 另一個類似的磁碟 I/O 疑難排解套件是以 [Windows 效能記錄器](https://docs.microsoft.com/windows-hardware/test/wpt/introduction-to-wpr) \(部分機器翻譯\) 的內建設定檔形式提供。
  
> [!NOTE]  
> 防毒程式可能會降低磁碟存取的速度。 若要加快存取速度，請從使用中的病毒掃描排除錯誤訊息中所指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料檔案。 您可以使用 [fltmc.exe 命令列公用程式](https://docs.microsoft.com/windows-hardware/drivers/ifs/development-and-testing-tools#fltmcexe-control-program) \(英文\) 來查詢安裝在系統上的所有篩選器驅動程式，並了解其在資料庫檔案儲存體路徑上所執行的功能。 
  
如需 I/O 錯誤的詳細資訊，請參閱 [Microsoft SQL Server I/O Basics, Chapter 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10)) (第 2 章 Microsoft SQL Server I/O 基本概念) 以及 [https://support.microsoft.com/kb/897284/en-us](https://support.microsoft.com/kb/897284/en-us) 的知識庫文章。  
  
