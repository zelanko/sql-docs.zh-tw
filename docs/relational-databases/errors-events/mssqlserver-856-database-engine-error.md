---
description: MSSQLSERVER_856
title: MSSQLSERVER_856
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 856 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: f94f6f4e8f8eebee48bbb0c2a6d0faefa4218c25
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418758"
---
# <a name="mssqlserver_856"></a>MSSQLSERVER_856
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細資料

|屬性|值|
|---|---|
|產品名稱|SQL Server|
|事件識別碼|856|
|事件來源|MSSQLSERVER|
|元件|SQLEngine|
|符號名稱|BAD_MEMORY_CLEAN_DATABASE_PAGE|
|訊息文字|SQL Server 在資料庫 '%ls'，檔案識別碼：%u，頁面識別碼：%u，記憶體位址：0x%I64x 中偵測到硬體記憶體損毀，且已經成功復原此頁面|
||

## <a name="explanation"></a>說明

此訊息表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在緩衝集區外的快取物件中偵測到錯誤的記憶體頁面。 這則訊息是在支援從記憶體錯誤中復原的系統上產生。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 藉由捨棄未修改的損毀記憶體頁面來更正這些記憶體錯誤，並記錄此錯誤訊息。 如果損毀的記憶體頁面已修改 (已變更)，則會引發錯誤 824 ([MSSQLSERVER_824](mssqlserver-824-database-engine-error.md))

## <a name="user-action"></a>使用者動作

您應該執行硬體或系統檢查，以判斷是否存在記憶體或 CPU 問題。 請確定所有系統驅動程式、作業系統更新及硬體更新已套用至系統。 請考慮執行任何硬體製造商診斷，包括記憶體相關測試。 每當看到此錯誤時，請考慮針對此執行個體中的所有資料庫執行 `DBCC CHECKDB`。

## <a name="more-information"></a>詳細資訊

在具有較新硬體且執行 Windows Server 2012 或更新版本的電腦上，硬體可通知作業系統和應用程式有關記憶體頁面 (作業系統頁面) 已標示為錯誤或損毀。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之類的應用程式可使用下列 API 集合來註冊這些錯誤記憶體頁面通知：

- `GetMemoryErrorHandlingCapabilities`
- `RegisterBadMemoryNotification`
- `BadMemoryCallbackRoutine`

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更新版本中新增了對這些通知的支援。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動期間，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會檢查硬體是否支援這項新功能。 此外，您會在錯誤記錄檔中收到下列訊息：

> \<Datetime> 伺服器電腦支援記憶體錯誤復原。 SQL 記憶體保護已啟用，可從記憶體損毀中復原。

目前，只有緩衝集區會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 收到這些通知時採取動作。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 收到通知時，其必須逐一查看整個緩衝區集區，並探索每個已配置緩衝區的位址。 然後，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 `QueryWorkingSetEX` API 來檢查支援資料頁的任何記憶體頁面是否標示為錯誤。 如果報告有任何損毀，則對應到此記憶體頁面的 `PSAPI_WORKING_SET_EX_BLOCK` 輸出結構會將其成員 bad 設定為 1。

如果該緩衝集區或資料頁目前未變更或未處理 I/O，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可捨棄及取消認可資料頁。 然後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會記錄下列訊息：

> SQL Server 在資料庫 '%ls'，檔案識別碼：%u，頁面識別碼：%u，記憶體位址：0x%I64x 中偵測到硬體記憶體損毀，且已經成功復原此頁面。

當查詢再次要求該資料頁時，緩衝集區可從磁碟讀回資料頁，並將內容帶回緩衝集區。 頁面的磁碟上版本也可能處於損毀狀態。 在此情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會記錄其他錯誤，例如錯誤 824。

如果錯誤頁面不是由緩衝集區所使用，而是由某些其他快取物件或結構所使用，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會記錄下列訊息：

> 偵測到無法更正的硬體記憶體損毀。 系統可能會變得不穩定。 如需詳細資料，請檢查 Windows 事件記錄檔。

如果伺服器回報記憶體錯誤，即應該洽詢電腦硬體廠商，並執行適當的動作，例如執行記憶體診斷、更新 BIOS 和韌體，以及更換損壞的記憶體模組。

您可使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 追蹤旗標 849，以防止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 向作業系統註冊記憶體錯誤通知。 但是，請注意，啟用追蹤旗標 849 會導致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法從作業系統接收錯誤記憶體通知。 因此，不建議在一般情況下使用此追蹤旗標。

此外，請注意，根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在支援的硬體上收到這些通知。

您也應該注意，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 註冊這些記憶體錯誤通知時，延遲寫入器系統處理序不會執行固定的頁面檢查。 如需固定頁面檢查的詳細資訊，請參閱[如何針對 SQL Server 中的訊息 832 (固定頁面已變更) 進行疑難排解](https://support.microsoft.com/help/2015759)。
