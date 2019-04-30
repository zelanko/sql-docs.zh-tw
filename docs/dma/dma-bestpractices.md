---
title: Data Migration assistant (SQL Server) 的最佳做法 |Microsoft Docs
description: 了解使用 Data Migration Assistant 移轉 SQL Server 資料庫的最佳做法
ms.custom: ''
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
manager: craigg
ms.openlocfilehash: cb355cbe1e32c97e59d61eb55ca70023b03acd6b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63154628"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>執行 Data Migration Assistant 的最佳做法
本文提供安裝、 評估和移轉一些最佳作法資訊。

## <a name="installation"></a>安裝
未安裝，並直接在 SQL Server 主機電腦上執行 Data Migration Assistant。

## <a name="assessment"></a>評估
- 在生產環境資料庫上執行評量，在非尖峰時段。
- 執行**相容性問題**並**新功能建議**分別可縮短評估期間的評定。

## <a name="migration"></a>移轉
- 在非尖峰時間期間移轉的伺服器。

- 當移轉的資料庫，提供可以存取來源伺服器與目標伺服器的單一共用位置，並盡可能避免複製作業。 複製作業可能會造成延遲取決於備份檔案的大小。 複製作業也會增加移轉將會因為額外的步驟而失敗的機會。 提供單一位置時，Data Migration Assistant 會略過複製作業。
 
    此外，務必提供正確的權限的共用資料夾以避免移轉失敗。 此工具中指定正確的權限。 如果網路服務的認證下執行的 SQL Server 執行個體，提供在共用資料夾上正確的權限給 SQL Server 執行個體之電腦帳戶。

- 連接到來源和目標伺服器時，啟用加密連接。 使用 SSL 加密可提高之間透過網路傳輸資料移轉小幫手和 SQL Server 執行個體，也就是有幫助，尤其是當移轉 SQL 登入的資料的安全性。 如果不使用 SSL 加密，網路遭到入侵，攻擊者所要移轉的 SQL 登入無法取得攔截及/或修改在即時由攻擊者。

    但是，如果所有的存取都與安全的內部網路組態有關，則可能不需要加密。 啟用加密會降低效能，因為這是加密和解密的封包所需的額外負荷。 如需詳細資訊，請參閱 [加密 SQL Server 的連接](https://go.microsoft.com/fwlink/?linkid=832513)。
