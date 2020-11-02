---
description: MSSQLSERVER_5180
title: MSSQLSERVER_5180
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5180 (Database Engine error)
ms.assetid: ''
author: rgward
ms.author: ramakoni
ms.openlocfilehash: cbdc30c1e05d50bb20df3f9e3ebf54097c770743
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418740"
---
# <a name="mssqlserver_5180"></a>MSSQLSERVER_5180
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細資料

|屬性|值|
|---|---|
|產品名稱|SQL Server|
|事件識別碼|5180|
|事件來源|MSSQLSERVER|
|元件|SQLEngine|
|符號名稱|DSK_BAD_FCB_FILEID|
|訊息文字|無法為無效檔案識別碼 %d 於資料庫 '%.*ls' 中開啟檔案控制銀行 (File Control Bank，FCB)。 請確定檔案的位置， 執行 DBCC CHECKDB。|
||

## <a name="explanation"></a>說明

當 [!INCLUDE[ssDENoVersion](../../includes/ssdenoversion_md.md)] 參考了無效的檔案識別碼時，查詢或作業可能會失敗，並出現錯誤 5180。 這是一個範例：

> 訊息 5180，層級 22，狀態 1，行 1  
無法為無效檔案識別碼 %d 於資料庫 '%.*ls' 中開啟檔案控制銀行 (File Control Bank，FCB)。 請確定檔案的位置， 執行 DBCC CHECKDB。

由於引發錯誤的嚴重性為 22，因此使用者的工作階段將會中斷連線。 此錯誤訊息會以 EventID = 5180 的形式寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔和 Windows 應用程式事件記錄檔中。

## <a name="possible-causes"></a>可能的原因

在許多不同的情況下，當參考頁面識別碼時，[!INCLUDE[ssDENoVersion](../../includes/ssdenoversion-md.md)] 會參考檔案識別碼 (因為檔案識別碼是頁面識別碼的第一個部分)。 如果基於任何原因，所參考的檔案識別碼小於 0，或不是資料庫中的有效檔案識別碼 (依據系統目錄檢視中所列的有效檔案識別碼，例如 sys.database_files)，則可能會發生 5180 錯誤。

其中一個可能原因是儲存的檔案識別碼無效。 由於資料列中的轉送記錄會參考另一個頁面，因此在存取該頁面且檔案識別碼無效時，可能會發生 5180 錯誤。 這種情況會是含有轉送記錄的頁面上發生資料庫損毀錯誤。 (在此範例中，`DBCC CHECKDB` 會報告訊息 8993)。

另一個範例是，儲存在下一頁或上一頁識別碼頁首中作為部分頁面識別碼的無效檔案識別碼。 這個欄位用來連結一系列的頁面 (例如在叢集索引中)。 如果上一頁或下一頁的檔案識別碼無效，則當引擎必須參考此識別碼以周遊至下一頁或上一頁時，就可能會發生 5180 錯誤。 (在此範例中，`DBCC CHECKDB` 會報告訊息 8981)。

如果問題不是由於儲存的頁面識別碼損毀而導致檔案識別碼無效，則問題可能是出在 [!INCLUDE[ssDENoVersion](../../includes/ssdenoversion-md.md)]。

## <a name="user-action"></a>使用者動作

若遇到這個錯誤，則應該針對錯誤訊息中所列的資料庫執行 `DBCC CHECKDB`。 若發現錯誤，則應該從已知的正確備份進行還原。 若無法從備份還原，則另一個選項是使用其輸出所建議的 `DBCC CHECKDB` 修復選項。 在大部分情況下，修復此類型的錯誤將會導致資料遺失。 如需使用和導致資料庫損毀問題的詳細資訊，請參閱下列文章：[如何針對 DBCC CHECKDB 報告的資料庫一致性錯誤進行疑難排解](https://support.microsoft.com/kb/2015748)。

如果 `DBCC CHECKDB` 未回報任何錯誤，但問題仍持續發生，則應該與 Microsoft 技術支援人員連絡以取得協助。 請準備好提供發生 5180 錯誤的查詢。 如需如何判斷哪個查詢發生錯誤的資訊，請參閱[詳細資訊](#more-information)一節。

## <a name="more-information"></a>詳細資訊

檔案控制區 (FCB) 是一種內部記憶體結構，可追蹤與資料庫建立關聯的檔案其重要資訊。 檔案識別碼則用來唯一識別資料庫的 FCB。 如果伺服器引擎嘗試參考的檔案識別碼無效，就找不到觸發 5180 錯誤狀況的 FCB 結構。

若要找出發生此錯誤的查詢，您可使用下列技術：

- 若為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 和更新版本，請查看 system_health 工作階段是否有錯誤的記錄，其中應該包含查詢文字。 如需 system_health 工作階段的詳細資訊，請參閱資源：[支援 SQL Server 2008：system_health 工作階段](https://techcommunity.microsoft.com/t5/sql-server-support/supporting-sql-server-2008-the-system-health-session/ba-p/315509) (英文)。
- 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler，並擷取 `SQL:BatchStarting`、`RPC:Starting` 及例外狀況事件。 請針對與例外狀況事件建立關聯的工作階段，尋找 5180 例外狀況事件之前的查詢。
