---
title: 資料移轉小幫手的最佳做法
description: 瞭解使用 Data Migration Assistant 遷移 SQL Server 資料庫的最佳作法，包括安裝、評估和遷移的相關資訊。
ms.custom: seo-lt-2019
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Best Practices
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.openlocfilehash: 440d6d12ed639d158ad0309209b60daa56e08322
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727779"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>執行 Data Migration Assistant 的最佳做法 (機器翻譯)
本文提供安裝、評估和遷移的一些最佳作法資訊。

## <a name="installation"></a>安裝
請勿直接在 SQL Server 主機電腦上安裝和執行 Data Migration Assistant。

## <a name="assessment"></a>評量
- 在非尖峰時間執行生產資料庫的評量。
- 分別執行 **相容性問題** 和 **新功能建議** 評定，以減少評量的持續時間。

## <a name="migration"></a>遷移
- 在非尖峰時間時遷移伺服器。

- 在遷移資料庫時，請提供來源伺服器和目標伺服器可存取的單一共用位置，並盡可能避免複製作業。 複製作業可能會根據備份檔案的大小來引入延遲。 由於有額外的步驟，因此複製作業也可增加遷移失敗的機率。 當提供單一位置時，Data Migration Assistant 會略過複製操作。
 
    此外，請務必提供共用資料夾的正確許可權，以避免發生遷移失敗。 在工具中指定正確的許可權。 如果 SQL Server 實例是以 Network Service 認證執行，請將共用資料夾上的正確許可權提供給 SQL Server 實例的電腦帳戶。

- 連接到來源和目標伺服器時，啟用加密連接。 使用 TLS 加密可提升 Data Migration Assistant 與 SQL Server 實例之間跨網路傳輸資料的安全性，這在遷移 SQL 登入時特別有用。 如果未使用 TLS 加密，且網路遭到攻擊者入侵，則遷移的 SQL 登入可能會被攻擊者即時攔截及/或修改。

    但是，如果所有的存取都與安全的內部網路組態有關，則可能不需要加密。 啟用加密會降低效能，因為加密和解密封包所需的額外負荷。 如需詳細資訊，請參閱 [SQL Server 的加密連接](/previous-versions/sql/sql-server-2008-r2/ms189067(v=sql.105))。
    
- 在遷移資料之前，請先檢查源資料庫與目標資料庫的不受信任條件約束。 在遷移之後，再次分析目標資料庫，以查看是否有任何條件約束在資料移動時變成不受信任。 視需要修正不受信任的條件約束。 保持不受信任的條件約束可能會導致執行計畫不佳，而且可能會影響效能。