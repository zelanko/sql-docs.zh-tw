---
title: 資料移轉小幫手 (SQL Server) 的最佳作法 |Microsoft 文件
ms.custom: ''
ms.date: 06/02/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Best Practices
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 8a1b184a6a280b328df35ea04a1ab6caf996c7c8
ms.sourcegitcommit: 6fe7b5e8818bd0d94fce693c560d63cc6883d76f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34758108"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>執行資料移轉小幫手的最佳作法
本文提供安裝、 評估及移轉下列最佳做法的資訊。

## <a name="installation"></a>安裝
請勿安裝並直接在 SQL Server 主機電腦上執行資料移轉小幫手。

## <a name="assessment"></a>評估
- 在非尖峰時間，在實際執行資料庫上執行評估。
- 執行**相容性問題**和**新功能建議**分開來縮短評估期間的評估。

## <a name="migration"></a>移轉
- 在非尖峰期間移轉的伺服器。
- 當移轉資料庫，提供可以存取來源伺服器與目標伺服器上，為單一的共用位置，並儘可能避免複製作業。 複製作業可能會導致延遲根據備份檔案的大小。 複製作業也會增加移轉將會因為額外的步驟，而失敗的機會。 提供單一位置時，資料移轉小幫手會略過複製作業。
 
    此外，務必要提供給共用資料夾的正確權限，直到避免移轉失敗。 此工具中指定正確的權限。 如果網路服務認證下執行的 SQL Server 執行個體，提供共用資料夾上正確的權限給 SQL Server 執行個體之電腦帳戶。

- 連接到來源和目標伺服器時，啟用加密連接。 使用 SSL 加密可提高資料移轉小幫手 」 與 「 SQL Server 執行個體，也就是有幫助，尤其是移轉 SQL 登入之間的網路上傳輸資料的安全性。 如果不使用 SSL 加密，網路遭到入侵，攻擊者所要移轉的 SQL 登入無法取得攔截及/或修改在即時操作的攻擊者。

    但是，如果所有的存取都與安全的內部網路組態有關，則可能不需要加密。 啟用加密會降低效能，因為這是必要的加密和解密的封包的額外負荷。 如需詳細資訊，請參閱[加密對 SQL Server 的連線](https://go.microsoft.com/fwlink/?linkid=832513)。
