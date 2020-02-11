---
title: MSSQLSERVER_833 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 833 (Database Engine error)
ms.assetid: 14129cc4-be80-4772-9e3f-0e5da4d0696b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: db70d1757073a48ab09f31cfb3570570e54a48cd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62762079"
---
# <a name="mssqlserver_833"></a>MSSQLSERVER_833
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|833|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|BUF_LONG_IO|  
|訊息文字|SQL Server 在資料庫`[%ls] (%d)`中的檔案 [% ls] 上發現% d 次發生的 i/o 要求超過% d 秒。  作業系統檔案控制代碼為 0x%p。  最新的長 I/O 的位移為: %#016I64x。|  
  
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
  
 例如，在執行  **的電腦上，** Average Disk Sec/Transfer[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時間通常少於 15 毫秒。 如果 **Average Disk Sec/Transfer** 值增加，表示 I/O 子系統並未以最佳的方式應付 I/O 需要。  
  
> [!NOTE]  
>  防毒程式可能會降低磁碟存取的速度。 若要加快存取速度，請從使用中的病毒掃描排除錯誤訊息中所指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料檔案。  
  
 如需 I/O 錯誤的詳細資訊，請參閱 [Microsoft SQL Server I/O Basics, Chapter 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10)) (第 2 章 Microsoft SQL Server I/O 基本概念) 以及 [https://support.microsoft.com/kb/897284](https://support.microsoft.com/kb/897284) 的知識庫文章。  
  
  
