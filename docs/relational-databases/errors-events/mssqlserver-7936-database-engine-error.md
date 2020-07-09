---
title: MSSQLSERVER_7936 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7936 (Database Engine error)
ms.assetid: d78fc8a9-d173-4801-bb32-ed6a29257f08
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c743bfdae50b15d7d06015fdcf40f2fb49baf179
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767926"
---
# <a name="mssqlserver_7936"></a>MSSQLSERVER_7936
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|7936|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC2_FS_ORPHANED_COLUMN_DIRECTORY|  
|訊息文字|資料表錯誤：物件識別碼 O_ID，索引識別碼 I_ID，分割區識別碼 PN_ID 的資料行識別碼 C_ID 存在 Filestream 目錄，但是該資料行並非 Filestream 資料行。|  
  
## <a name="explanation"></a>說明  
在 DBCC CHECKDB 執行期間，系統已找到指定之資料行的 FILESTREAM 目錄。但是，該資料行不是 **FILESTREAM** 資料行。  
  
## <a name="user-action"></a>使用者動作  
  
### <a name="look-for-hardware-failure"></a>尋找硬體故障  
請執行硬體診斷並更正所有問題， 同時檢查 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 系統和應用程式記錄檔以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，以查看錯誤發生的原因是否為硬體故障。 請修正前述記錄檔中所包含的任何硬體相關問題。  
  
若有持續發生的資料損毀問題，請嘗試抽換不同的硬體元件以隔離問題。 請檢查以確認系統並未啟用磁碟控制器上的寫入快取功能。 如果您懷疑寫入快取就是問題所在，請與您的硬體廠商連絡。  
  
最後，切換到新的硬體系統可能也會有幫助。 此切換作業可能包括重新格式化磁碟機以及重新安裝作業系統。  
  
### <a name="restore-from-backup"></a>還原備份  
如果問題與硬體無關，而且確定有未受影響的備份可以使用，請利用該備份來還原資料庫。  
  
### <a name="run-dbcc-checkdb"></a>執行 DBCC CHECKDB  
不適用。 此錯誤無法自動修復。 如果無法從備份還原資料庫，請連絡 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客戶服務及支援中心 (CSS)。  
  
