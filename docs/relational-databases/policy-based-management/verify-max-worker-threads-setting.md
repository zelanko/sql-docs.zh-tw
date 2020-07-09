---
title: 驗證最大工作者執行緒設定 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 2d94adfd-3ba1-493a-b29a-b436f9d583df
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: cc1e6d32a8318d30f699e896999245e586fc5db2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773108"
---
# <a name="verify-max-worker-threads-setting"></a>確認最大工作者執行緒設定
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此規則會檢查 max worker threads server 選項中是否可能有不正確的設定。 將 max worker threads 選項設定為很小的值可能會阻礙足夠的執行緒及時服務內送用戶端要求，而且可能會導致執行緒資源用盡。 但是，將此選項設定為較大的值可能會浪費位址空間，因為每一個使用中執行緒都會在 64 位元伺服器上最多耗用 4 MB 空間。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 將 max worker threads 選項設成 0。 如此可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 根據使用者要求來自動判斷 active worker threads 的正確數目。  
  
## <a name="for-more-information"></a>詳細資訊  
 [設定 max worker threads 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
