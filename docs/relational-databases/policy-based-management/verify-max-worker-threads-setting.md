---
title: 驗證最大工作者執行緒設定 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 2d94adfd-3ba1-493a-b29a-b436f9d583df
caps.latest.revision: 17
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f171d85ccaabfc6e7368f15ae826a7fc6a78e416
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="verify-max-worker-threads-setting"></a>確認最大工作者執行緒設定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此規則會檢查 max worker threads server 選項中是否可能有不正確的設定。 將 max worker threads 選項設定為很小的值可能會阻礙足夠的執行緒及時服務內送用戶端要求，而且可能會導致執行緒資源用盡。 但是，將此選項設定為較大的值可能會浪費位址空間，因為每一個使用中執行緒都會在 64 位元伺服器上最多耗用 4 MB 空間。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 將 max worker threads 選項設成 0。 如此可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 根據使用者要求來自動判斷 active worker threads 的正確數目。  
  
## <a name="for-more-information"></a>詳細資訊  
 [設定 max worker threads 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
