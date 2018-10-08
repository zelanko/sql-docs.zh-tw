---
title: 正確的親和性遮罩和親和性輸入與輸出遮罩重疊 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1a0da6df-57ff-4f3f-aae9-2fbc4897508c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 05652024c7d887e7bc34119f3e529c7f404324bc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47623366"
---
# <a name="correct-affinity-mask-and-affinity-input-and-output-mask-overlap"></a>正確的親和性遮罩和親和性輸入與輸出遮罩重疊
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
  
