---
title: 資料移轉小幫手的最佳做法
description: 使用資料移轉助手瞭解移至 SQL Server 資料庫的最佳做法
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
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: f2bfbb79a8a4803bb56e3dce85f575e8cf257b4a
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388157"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>適用於執行 Data Migration Assistant 的最佳做法
本文提供了一些用於安裝、評估和遷移的最佳做法資訊。

## <a name="installation"></a>安裝
不要在 SQL Server 主機上直接安裝和運行數據遷移助手。

## <a name="assessment"></a>評量
- 在非高峰時間對生產資料庫運行評估。
- 分別執行**相容性問題和****新功能建議**評估,以減少評估持續時間。

## <a name="migration"></a>遷移
- 在非高峰時間遷移伺服器。

- 遷移資料庫時,提供源伺服器和目標伺服器可訪問的單個共用位置,並盡可能避免複製操作。 複製操作可能會根據備份檔的大小引入延遲。 複製操作還會增加遷移由於額外步驟而失敗的可能性。 當提供單個位置時,數據遷移助手會繞過複製操作。
 
    此外,請確保向共享資料夾提供正確的許可權,以避免遷移失敗。 該工具中指定了正確的許可權。 如果 SQL Server 實體在網路服務認證下運行,則將共用資料夾的正確權限授予 SQL Server 實體的電腦帳戶。

- 連接到源伺服器和目標伺服器時啟用加密連接。 使用 TLS 加密可提高資料遷移助手和 SQL Server 實例之間透過網路傳輸的數據的安全性,這在遷移 SQL 登錄時尤其有益。 如果未使用 TLS 加密,並且網路受到攻擊者的威脅,則正在遷移的 SQL 登錄可能會被攻擊者即時攔截和/或修改。

    但是，如果所有的存取都與安全的內部網路組態有關，則可能不需要加密。 啟用加密會降低性能,因為加密和解密數據包需要額外的開銷。 關於詳細資訊,請參考 [加密到 SQL 伺服器的連線](https://go.microsoft.com/fwlink/?linkid=832513)。
    
- 在遷移數據之前,請檢查源資料庫和目標資料庫上的不受信任的約束。 遷移后,請再次分析目標資料庫,以查看作為數據移動的一部分,是否有任何約束變得不受信任的約束。 根據需要修復不受信任的約束。 使約束不受信任可能會導致執行計劃不佳,並且可能會影響性能。
