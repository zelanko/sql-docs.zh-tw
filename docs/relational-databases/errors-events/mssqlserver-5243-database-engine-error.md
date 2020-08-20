---
description: MSSQLSERVER_5243
title: MSSQLSERVER_5243 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5243 (Database Engine error)
ms.assetid: e04a1934-e57d-420e-ac79-97071745824e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2575d81f09ccb3ac4aceb2396f5db0f8d9bee451
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470980"
---
# <a name="mssqlserver_5243"></a>MSSQLSERVER_5243
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|5243|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|執行內部作業期間偵測到不一致性。 請連絡技術支援部門。 參考編號 %ld。|  
  
## <a name="explanation"></a>說明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在記憶體儲存引擎結構中偵測到結構不一致。  
  
## <a name="user-action"></a>使用者動作  
尋找硬體故障。 請執行硬體診斷並更正所有問題， 同時檢查 Windows 系統和應用程式記錄檔以及 SQL Server 錯誤記錄檔，以查看錯誤發生的原因是否為硬體故障。 請修正記錄檔中所包含的任何硬體相關問題。

若有持續發生的資料損毀問題，請嘗試抽換不同的硬體元件以隔離問題。 請檢查以確認系統的磁碟控制器並未啟用寫入快取功能。 如果您懷疑寫入快取就是問題所在，請與您的硬體廠商連絡。

最後，切換到新的硬體系統可能也會有幫助。 此切換作業可能包括重新格式化磁碟機以及重新安裝作業系統。

從備份還原：如果問題與硬體無關，而且有已知的完好備份可供使用，請從該備份還原資料庫。

執行 DBCC CHECKDB：如果沒有完好備份可供使用，請執行不含 REPAIR 子句的 DBCC CHECKDB，以判斷損毀的範圍。 DBCC CHECKDB 將建議適用的 REPAIR 子句。 接著，請執行內含適當 REPAIR 子句的 DBCC CHECKDB，以修復損毀的部分。

> **不支援警示標記！！！！** 
> **不支援 tr 標記！！！！** 
> **不支援 tr 標記！！！！**

如果執行含 REPAIR 子句的 DBCC CHECKDB 並未修正這個問題，請與您的主要支援提供者連絡，再執行這個陳述式。
  
## <a name="see-also"></a>另請參閱  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[資料庫檔案與檔案群組](~/relational-databases/databases/database-files-and-filegroups.md)  
  
