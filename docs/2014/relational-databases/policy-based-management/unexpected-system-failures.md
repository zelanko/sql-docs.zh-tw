---
title: 非預期的系統失敗 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b791ba0e3f709288a4e2c5b6add4e74e15d56dee
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85047784"
---
# <a name="unexpected-system-failures"></a>非預期的系統失敗
  這個規則會檢查電腦事件記錄檔中是否有 SYSTEM 事件 6008。 此事件表示非預期的系統關機。 系統可能不穩定，而且可能無法提供主控 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體所需的穩定性和完整性。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 立即找出非預期伺服器重新啟動的原因，或是將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體移到另一部電腦。  
  
  
