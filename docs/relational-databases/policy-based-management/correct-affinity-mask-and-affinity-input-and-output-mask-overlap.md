---
title: 正確的親和性遮罩與親和性 I/O 遮罩重疊原則
description: 了解如何啟用一個原則，檢查 SQL Server 的執行個體是否有一或多個已指派的處理器，可用於 SQL Server 中原則式管理的親和性遮罩和親和性 I/O 遮罩選項。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1a0da6df-57ff-4f3f-aae9-2fbc4897508c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ee4cc32adeb69a3cb60c4087067d9b5a9aad121e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85654715"
---
# <a name="correct-affinity-mask-and-affinity-input-and-output-mask-overlap"></a>Correct Affinity Mask and Affinity Input and Output Mask Overlap
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  這個規則會檢查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體是否有一或多個指派給搭配 affinity mask 和 affinity I/O mask 選項使用的處理器。 在具有一個以上處理器的電腦中，affinity mask 和 affinity I/O mask 選項是用來指派 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所使用的 CPU。 使用 affinity mask 和 affinity I/O mask 來啟用 CPU 可能會強制處理器過度使用而使效能變慢。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 當您指定 affinity mask 或 affinity I/O mask 選項時，您應該指定這兩者，但是每一個 CPU 不能啟用超過一次。  
  
 請勿同時在 affinity mask 選項和 affinity I/O mask 選項內啟用相同的 CPU。 對應到每個 CPU 的位元應屬於下列三種情況之一：  
  
-   affinity mask 選項和 affinity I/O mask 選項內的 0  
  
-   affinity mask 選項內的 0 和 affinity I/O mask 選項內的 1  
  
-   affinity mask 選項內的 1 和 affinity I/O mask 選項內的 0  
  
## <a name="for-more-information"></a>詳細資訊  
 [affinity mask 伺服器組態選項](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)  
  
 [affinity Input-Output mask 伺服器組態選項](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)  
  
 [affinity64 mask 伺服器組態選項](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md)  
  
 [affinity64 輸入輸出伺服器組態選項](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
