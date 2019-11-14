---
title: 資料移轉小幫手的最佳做法
description: 瞭解使用 Data Migration Assistant 遷移 SQL Server 資料庫的最佳作法
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
ms.openlocfilehash: ef953aa369e831e47d38db403b982919bd4bd830
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056550"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>執行 Data Migration Assistant 的最佳做法
本文提供安裝、評估和遷移的一些最佳作法資訊。

## <a name="installation"></a>Installation
請勿直接在 SQL Server 主機電腦上安裝和執行 Data Migration Assistant。

## <a name="assessment"></a>評估
- 在非尖峰時間執行生產資料庫的評量。
- 分別執行**相容性問題**和**新的功能建議**評量，以減少評量的持續時間。

## <a name="migration"></a>移轉
- 在非尖峰時間遷移伺服器。

- 在遷移資料庫時，請提供來源伺服器和目標伺服器可存取的單一共用位置，並盡可能避免複製作業。 複製作業可能會根據備份檔案的大小來引入延遲。 複製作業也會增加因額外步驟而導致遷移失敗的機率。 當提供單一位置時，Data Migration Assistant 會略過複製作業。
 
    此外，請確定為共用資料夾提供正確的許可權，以避免發生遷移失敗。 正確的許可權是在工具中指定。 如果 SQL Server 實例是以網路服務認證執行，請將共用資料夾的正確許可權提供給 SQL Server 實例的電腦帳戶。

- 連接到來源和目標伺服器時，啟用加密連接。 使用 SSL 加密可提高 Data Migration Assistant 和 SQL Server 實例之間，在網路上傳輸之資料的安全性，這在遷移 SQL 登入時特別有用。 如果未使用 SSL 加密，且網路受到攻擊者危害，則要遷移的 SQL 登入可能會受到攻擊者即時攔截及/或修改。

    但是，如果所有的存取都與安全的內部網路組態有關，則可能不需要加密。 啟用加密會降低效能，因為加密和解密封包所需的額外負荷。 如需詳細資訊，請參閱 [SQL Server 的加密連接](https://go.microsoft.com/fwlink/?linkid=832513)。
