---
description: 使用者資料庫上的對稱金鑰
title: 使用者資料庫上的對稱金鑰 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3333ab5b-2518-4753-a0a8-57df5e5af74f
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c7882b4f3f425b600e3ef57fa836ffffd6756289
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88380964"
---
# <a name="symmetric-keys-on-user-databases"></a>使用者資料庫上的對稱金鑰
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此規則會檢查長度少於 128 個位元組的金鑰是否不使用 RC2 或 RC4 加密演算法。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 使用 AES 128 位元或更大的位元來建立對稱金鑰進行資料加密。 如果作業系統不支援 AES，請使用 3DES。  
  
## <a name="for-more-information"></a>詳細資訊  
 [選擇加密演算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
