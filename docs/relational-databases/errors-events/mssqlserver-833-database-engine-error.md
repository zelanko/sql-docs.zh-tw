---
title: MSSQLSERVER_833 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 833 (Database Engine error)
ms.assetid: 14129cc4-be80-4772-9e3f-0e5da4d0696b
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fd32f5eb35a0d938e60e3ea43aa8428a4b458930
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver833"></a>MSSQLSERVER_833
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|833|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|BUF_LONG_IO|  
|訊息文字|SQL Server 在資料庫 `[%ls] (%d)` 中的檔案 [%ls] 上發現 %d 次花費 %d 秒以上才完成的 I/O 要求。  作業系統檔案控制代碼為 0x%p。  最新的長 I/O 的位移為: %#016I64x。|  
  
## <a name="explanation"></a>說明  
此訊息表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已經從磁碟發出讀取或寫入要求，且該要求花費超過 15 秒才傳回。 此錯誤是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 回報，並且表示 IO 子系統發生問題。  
  
### <a name="possible-causes"></a>可能的原因  
造成此問題的原因可能是系統效能問題、硬體錯誤、韌體錯誤、裝置驅動程式問題，或篩選驅動程式介入 IO 處理序。  
  
## <a name="user-action"></a>使用者動作  
查看系統事件記錄檔中是否有與硬體相關的錯誤訊息，以便對此錯誤進行疑難排解。 同時，也查看硬體特定的記錄檔 (如果有的話)。  
  
使用「效能監視器」檢查下列計數器︰  
  
-   **Average Disk Sec/Transfer**  
  
-   **Average Disk Queue Length**  
  
-   **Current Disk Queue Length**  
  
例如，在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦上，**Average Disk Sec/Transfer** 時間通常少於 15 毫秒。 如果 **Average Disk Sec/Transfer** 值增加，表示 I/O 子系統並未以最佳的方式應付 I/O 需要。  
  
> [!NOTE]  
> 防毒程式可能會降低磁碟存取的速度。 若要加快存取速度，請從使用中的病毒掃描排除錯誤訊息中所指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料檔案。  
  
如需 I/O 錯誤的詳細資訊，請參閱 [Microsoft SQL Server I/O Basics, Chapter 2](http://go.microsoft.com/fwlink/?LinkId=69370) (第 2 章 Microsoft SQL Server I/O 基本概念)，以及位於 [http://support.microsoft.com/kb/897284/en-us](http://support.microsoft.com/kb/897284/en-us) 的知識庫文章。  
  

