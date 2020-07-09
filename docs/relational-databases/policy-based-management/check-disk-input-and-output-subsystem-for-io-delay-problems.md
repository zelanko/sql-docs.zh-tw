---
title: 檢查磁碟 IO 子系統的 IO 延遲問題
description: 了解如何透過檢查事件記錄檔中是否存在錯誤訊息 833 (SQL Server 進行原則式管理)，來啟用原則以檢查磁碟 IO 子系統中是否存在 IO 延遲問題。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 23863340-d8e0-48d6-928b-462745885d37
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f8c880438491f697d57134b5004129eef38a7fe8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749517"
---
# <a name="check-disk-input-and-output-subsystem-for-io-delay-problems"></a>檢查磁碟輸入輸出子系統的 IO 延遲問題
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  這個規則會檢查事件記錄檔中是否有錯誤訊息 833。 此訊息表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已經從磁碟發出讀取或寫入要求，且該要求花費超過 15 秒才傳回。 此錯誤是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 回報，並且表示磁碟 I/O 子系統發生問題。 延遲這麼長的時間會嚴重損害 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境的效能。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 查看系統事件記錄檔中是否有與硬體相關的錯誤訊息，以便對此錯誤進行疑難排解。 同時，也查看硬體特定的記錄檔 (如果有的話)。  
  
 使用「效能監視器」檢查下列計數器︰  
  
-   Average Disk Sec/Transfer  
  
-   Average Disk Queue Length  
  
-   Current Disk Queue Length  
  
 例如，在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦上，Average Disk Sec/Transfer 時間通常少於 15 毫秒。 如果 Average Disk Sec/Transfer 值增加，表示磁碟 I/O 子系統並未以最佳的方式應付 I/O 需要。  
  
## <a name="for-more-information"></a>詳細資訊  
   
  
 [Microsoft 知識庫文章 897284](https://go.microsoft.com/fwlink/?linkid=117743)  
  
 [SQL Server I/O 基本概念，第 2 章](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))
