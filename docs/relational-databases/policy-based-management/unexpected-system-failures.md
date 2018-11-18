---
title: 非預期的系統失敗 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: dde1e7592a3af09900cd656d7b6faafeab88f27d
ms.sourcegitcommit: ef6e3ec273b0521e7c79d5c2a4cb4dcba1744e67
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/10/2018
ms.locfileid: "51512663"
---
# <a name="unexpected-system-failures"></a>非預期的系統失敗
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  這個規則會檢查電腦事件記錄檔中是否有 SYSTEM 事件 6008。 此事件表示非預期的系統關機。 系統可能不穩定，而且可能無法提供主控 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體所需的穩定性和完整性。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 立即找出非預期伺服器重新啟動的原因，或是將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體移到另一部電腦。  
  
  
