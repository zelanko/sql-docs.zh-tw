---
title: 使用者資料庫上的對稱金鑰 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
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
ms.assetid: 3333ab5b-2518-4753-a0a8-57df5e5af74f
caps.latest.revision: 6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: be15cf6291d6cdeefe64f6dc6be77fe604dde30d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="symmetric-keys-on-user-databases"></a>使用者資料庫上的對稱金鑰
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此規則會檢查長度少於 128 個位元組的金鑰是否不使用 RC2 或 RC4 加密演算法。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 使用 AES 128 位元或更大的位元來建立對稱金鑰進行資料加密。 如果作業系統不支援 AES，請使用 3DES。  
  
## <a name="for-more-information"></a>詳細資訊  
 [選擇加密演算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
