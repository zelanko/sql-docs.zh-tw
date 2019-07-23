---
title: MSSQLSERVER_605 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 605 (Database Engine error)
ms.assetid: d8d3a22e-1ff8-48a4-891f-4c8619437e24
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7657c18708e9b54c33f15142c57782da671037f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903935"
---
# <a name="mssqlserver605"></a>MSSQLSERVER_605
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|605|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|WRONGPAGE|  
|訊息文字|嘗試提取邏輯頁 %S_PGID 失敗，資料庫：%d。 它屬於配置單位 %I64d，而非屬於 %I64d。|  
  
## <a name="explanation"></a>說明  
這個錯誤通常表示指定的資料庫發生頁面或配置損毀。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在讀取屬於資料表的頁面時，會循著頁面連結或利用索引配置對應 (IAM) 來偵測是否有損毀。 所有配置到給定資料表的頁面，都必須屬於與該資料表關聯的其中一個配置單位。 包含在頁首中的配置單位識別碼若與資料表的關聯配置單位識別碼不相符，便會引發此例外狀況。 錯誤訊息所列的第一個配置單位識別碼是存在頁首中的識別碼，而第二個配置單位值則是資料表的關聯識別碼。  
  
**資料損毀錯誤**  
  
嚴重性層級 21 表示資料可能已損毀。 原因大致包括：頁面鏈結損壞、IAM 損毀，或是該物件的 [sys.objects](~/relational-databases/system-catalog-views/sys-objects-transact-sql.md) 目錄檢視包含無效的項目。 這些錯誤通常是因為硬體或磁碟裝置驅動程式失效所造成。  
  
**暫時性錯誤**  
  
嚴重性層級 12 表示可能發生暫時性錯誤，亦即快取有問題而不代表磁碟上的資料損壞。 暫時性 605 錯誤可能是因為下列狀況所造成：  
  
-   作業系統向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 誤報 I/O 作業已完成；即使資料其實並未損毀也會顯示錯誤訊息。  
  
以最佳化工具提示 NOLOCK 執行查詢，或將交易隔離等級設定為 READ UNCOMMITTED。 使用 NOLOCK 的查詢或者 READ UNCOMMITTED 若嘗試讀取其他使用者正在搬移或變更的資料，便會發生 605 錯誤。 若要確認是否發生暫時性 605 錯誤，請稍後再執行一次查詢。 如需詳細資訊，請參閱這篇知識庫文章 [235880](https://support.microsoft.com/kb/235880/en-us)："You receive an "Error 605" error message when you run a query with the optimizer hint NOLOCK or you set the transaction isolation level to READ UNCOMMITTED in SQL Server" (當您使用最佳化器提示 NOLOCK 執行查詢，或在 SQL Server 中將交易隔離等級設定為 READ UNCOMMITTED 時，收到「錯誤 605」錯誤訊息)。  
  
一般而言，如果錯誤僅在資料存取期間發生，但後續的 DBCC CHECKDB 作業均順利完成而沒有錯誤，605 錯誤可能就是暫時性錯誤。  
  
## <a name="user-action"></a>使用者動作  
如果 605 錯誤並非暫時性錯誤，問題就非常嚴重，您必須執行下列工作加以更正：  
  
1.  執行下列查詢，找出與訊息中指定的配置單位關聯的資料表。 請將 `allocation_unit_id` 改為錯誤訊息中指定的配置單位。  
  
    USE`database_name`;  
  
    GO  
  
    SELECT au.allocation_unit_id, OBJECT_NAME(p.object_id) AS table_name, fg.name AS filegroup_name,  
  
    au.type_desc AS allocation_type, au.data_pages, partition_number  
  
    FROM sys.allocation_units AS au  
  
    JOIN sys.partitions AS p ON au.container_id = p.partition_id  
  
    JOIN sys.filegroups AS fg ON fg.data_space_id = au.data_space_id  
  
    WHERE au.allocation_unit_id = `allocation_unit_id` OR au.allocation_unit_id = `allocation_unit_id`  
  
    ORDER BY au.allocation_unit_id;  
  
    GO  
  
2.  找出與錯誤訊息中指定的第二個配置單位識別碼關聯的資料表之後，對該資料表執行不含 REPAIR 子句的 DBCC CHECKTABLE。  
  
3.  儘快執行不含 REPAIR 子句的 DBCC CHECKDB，以了解整個資料的損毀程度有多大。  
  
4.  檢查錯誤記錄檔中是否有經常伴隨 605 錯誤連帶發生的其他錯誤，並查看 Windows 事件記錄檔中是否有任何的系統或硬體相關問題。 請修正前述記錄檔中所包含的任何硬體相關問題。  
  
如果問題與硬體無關，請執行下列其中一項工作：  
  
1.  從未受影響的備份還原資料庫。 您可以利用分頁還原備份功能，只還原損毀的頁面。  
  
2.  根據您在步驟 3 中執行 DBCC CHECKDB 作業後獲得的建議，執行內含 REPAIR 子句的 DBCC CHECKDB 以修復損毀的部分。 如果執行含 REPAIR 子句的 DBCC CHECKDB 並未修正這個問題，請與您的主要支援提供者連絡，再執行這個陳述式。 請備妥 DBCC CHECKDB 的輸出結果以供檢閱。  
  
    > [!CAUTION]  
    > 如果不確定內含 REPAIR 子句之 DBCC CHECKDB 的效果為何，執行此陳述式之前請先與主要支援提供者連絡。  
  
## <a name="see-also"></a>另請參閱  
[DBCC CHECKTABLE &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checktable-transact-sql.md)  
  
