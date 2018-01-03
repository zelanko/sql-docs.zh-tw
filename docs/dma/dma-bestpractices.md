---
title: "資料移轉小幫手 (SQL Server) 的最佳作法 |Microsoft 文件"
ms.custom: 
ms.date: 10/04/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords: Data Migration Assistant, Best Practices
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f8842ca064494bc7ead99eb34d6ea2cc76bb2679
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="best-practices-for-running-data-migration-assistant"></a>執行資料移轉小幫手的最佳作法
本文提供下列安裝、 評估和移轉最佳作法資訊。

## <a name="installation"></a>安裝

請勿安裝並直接在 SQL Server 主機電腦上執行資料移轉小幫手。

## <a name="assessment"></a>評估

- 在非尖峰時間，在實際執行資料庫上執行評估。

- 執行**相容性問題**和**新功能建議**分開來縮短評估期間的評估。

## <a name="migration"></a>移轉

- 在非尖峰期間移轉的伺服器。

- 當移轉資料庫，提供可以存取來源伺服器與目標伺服器的單一共用位置，並儘可能避免複製作業。 複製作業可能會導致延遲根據備份檔案的大小。 複製作業也會增加額外的步驟，因為無法移轉的機會。 提供單一位置時，資料移轉小幫手會略過複製作業。
 
    也是確定所提供的共用資料夾的正確權限，直到避免移轉失敗。 此工具中指定正確的權限。 如果網路服務認證下執行的 SQL Server 執行個體，提供共用資料夾上正確的權限給 SQL Server 執行個體之電腦帳戶。

- 連接到來源和目標伺服器時，啟用加密連接。 使用 SSL 加密可提高資料移轉小幫手 」 與 「 SQL Server 執行個體之間的網路上傳輸資料的安全性。 這是有幫助，尤其是移轉 SQL 登入。 如果不使用 SSL 加密，網路遭到入侵，攻擊者所要移轉的 SQL 登入無法取得攔截及/或修改在即時操作的攻擊者。

    但是，如果所有的存取都與安全的內部網路組態有關，則可能不需要加密。 啟用加密會需要額外的負擔來加密和解密的封包而導致效能變慢。 如需詳細資訊，請參閱[加密對 SQL Server 的連線](https://go.microsoft.com/fwlink/?linkid=832513)。
