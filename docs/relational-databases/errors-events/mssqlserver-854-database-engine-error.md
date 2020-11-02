---
description: MSSQLSERVER_854
title: MSSQLSERVER_854
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 854 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: f0bf9061b452329280f0625bcc1339469372f4df
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418762"
---
# <a name="mssqlserver_854"></a>MSSQLSERVER_854
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細資料

|屬性|值|
|---|---|
|產品名稱|SQL Server|
|事件識別碼|854|
|事件來源|MSSQLSERVER|
|元件|SQLEngine|
|符號名稱|HARDWARE_MEMORY_SCRUBBER|
|訊息文字|電腦支援記憶體錯誤復原。 SQL 記憶體保護已啟用，可從記憶體損毀中復原|
||

## <a name="explanation"></a>說明

此訊息表示作業系統中的硬體支援從記憶體錯誤中復原此功能。 在具有較新硬體且執行 Windows Server 2012 或更新版本的電腦上，硬體可通知作業系統和應用程式有關記憶體頁面 (作業系統頁面) 已標示為錯誤或損毀。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之類的應用程式可使用下列 API 集合來註冊這些錯誤記憶體頁面通知：

- `GetMemoryErrorHandlingCapabilities`
- `RegisterBadMemoryNotification`
- `BadMemoryCallbackRoutine`

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 與更新版本中新增了對這些通知的支援。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動期間，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會檢查硬體是否支援這項新功能。 此外，您會在錯誤記錄檔中收到下列訊息：

> \<Datetime> 伺服器電腦支援記憶體錯誤復原。 SQL 記憶體保護已啟用，可從記憶體損毀中復原。

## <a name="user-action"></a>使用者動作

檢查是否遇到其他錯誤 (例如 855 與 856)，並採取適當的修正動作。

## <a name="more-information"></a>詳細資訊

您可使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 追蹤旗標 849，以防止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 向作業系統註冊記憶體錯誤通知。 但是，請注意，啟用追蹤旗標 849 會導致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法從作業系統接收錯誤記憶體通知。 因此，不建議在一般情況下使用此追蹤旗標。
