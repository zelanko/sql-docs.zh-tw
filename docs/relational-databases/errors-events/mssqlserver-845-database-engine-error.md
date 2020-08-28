---
description: MSSQLSERVER_845
title: MSSQLSERVER_845 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 845 (Database Engine error)
ms.assetid: 8fff6ad4-234c-44be-b123-e25d5e1cd63e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b4d474714579397d18e22f2c32cc540ff30d5ac0
ms.sourcegitcommit: a0245fdae1ff9045f587a3a67b72f34405d35a4f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88618077"
---
# <a name="mssqlserver_845"></a>MSSQLSERVER_845
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|845|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|BUFLATCH_TIMEOUT|  
|訊息文字|等候緩衝閂類型 %d (資料庫識別碼 %d，頁面 %S_PGID) 時發生逾時。|  
  
## <a name="explanation"></a>說明  
處理序一直等候要取得閂鎖，但該處理序等候到時間限制過期卻仍無法取得。 如果 I/O 作業完成需要花費太長時間 (通常是因為其他工作封鎖了系統處理序)，可能就會發生這種情形。 在某些情況下，這項錯誤可能是硬體故障的結果。  
  
## <a name="cause"></a>原因
此錯誤訊息取決於系統的整體環境。 下列任何一種情況都可能導致系統負荷過高：

- 硬體不符合輸入/輸出 (I/O) 和記憶體需求
- 未正確組態和測試的設定
- 效率不佳的設計

 當系統負載過重而無法符合工作負載需求時，可能會發生錯誤 845。 造成高負荷環境最常見的原因包括：

- 硬體問題
- 壓縮的磁碟區
- 非預設的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態設定
- 效率不佳的查詢或索引設計
- 頻繁的資料庫自動成長或自動壓縮作業

## <a name="user-action"></a>使用者動作  
請嘗試下列方法，以避免發生這項錯誤：  
  
- 判斷硬體是否出現瓶頸。 請參閱[找出瓶頸](../performance/identify-bottlenecks.md)，以開始解決問題。 如有必要，請升級硬體，使其能夠滿足環境組態、查詢和負載的需求。

- 確認所有硬體皆可正常運作。 檢查所有記錄的錯誤，據以執行硬體廠商提供的任何診斷事項。 查看錯誤記錄檔或事件記錄檔中相關聯的 I/O 失敗。 I/O 失敗通常表示磁碟功能有問題。  
- 確認磁碟區並未受到壓縮。 不支援在壓縮的磁碟機上儲存資料和記錄檔，請參閱[資料庫檔案與檔案群組](../databases/database-files-and-filegroups.md)。 如需有關壓縮磁碟機支援的詳細資訊，請參閱下列文章：[壓縮的磁碟區不支援 SQL Server 資料庫](https://support.microsoft.com/EN-US/help/231347) (英文)

- 當關閉下列所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態選項時，請查看錯誤訊息是否消失：
   - [優先權提升選項](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md)
   - [輕量型共用 (Fiber 模式) 選項](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)
   - [設定工作集大小選項](../../database-engine/configure-windows/set-working-set-size-server-configuration-option.md)

    如需詳細資訊，請參閱[做法：判斷適當的 SQL Server 組態設定](https://support.microsoft.com/EN-US/help/319942) (英文)

- 微調查詢以減少系統資源耗用。 效能微調有助於減輕系統負擔，並可縮短個別查詢的回應時間
- 將自動壓縮屬性設為 [關閉]，以降低資料庫大小變更時的額外負荷
- 確定自動成長選項的設定值夠大，以免遞增次數過於頻繁。 請將作業排程於離峰時段檢查資料庫中可用的空間量，再據以增加資料庫大小。
- 查看錯誤記錄檔，找出沒有產量的工作和其他重大錯誤。 請先解決這些錯誤，因為其可能指向根本問題的根本原因。
- 如果經常發生如判斷提示之類的重大錯誤，請解決這些問題
- 如果 845 錯誤訊息未經常發生，則可忽略錯誤