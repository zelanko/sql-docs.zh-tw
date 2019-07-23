---
title: 伺服器 public 權限 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4d600a5bf3e5667fdd3bd247e2e479a6c870ff21
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021708"
---
# <a name="server-public-permissions"></a>伺服器 public 權限
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此規則會判斷 public 伺服器角色是否有伺服器權限。 伺服器上建立的每一個登入都是 public 伺服器角色的成員。 如果符合這個條件，伺服器上的每個登入都具有伺服器權限。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 請勿將伺服器權限授與給伺服器 public 角色。  
  
> [!IMPORTANT]  
>  在安裝程式完成之後，**PUBLIC** 角色會擁有 [專用管理員連接]  以外之所有端點的 **CONNECT** 權限。 這是正常狀況，通常不應該變更 (存取權是使用建立新登入時自動授與的 **CONNECT SQL** 權限來控制)。  
  
### <a name="for-more-information"></a>如需詳細資訊  
 [保護 SQL Server 的安全](../../relational-databases/security/securing-sql-server.md)  
  
  
