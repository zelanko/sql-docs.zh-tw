---
title: 伺服器 public 權限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1389d712ff00438a2e6251315e8ebcc55e7fbff2
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43813914"
---
# <a name="server-public-permissions"></a>伺服器 public 權限
  此規則會判斷 public 伺服器角色是否有伺服器權限。 伺服器上建立的每一個登入都是 public 伺服器角色的成員。 如果符合這個條件，伺服器上的每個登入都具有伺服器權限。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 請勿將伺服器權限授與給伺服器 public 角色。  
  
> [!IMPORTANT]  
>  安裝程式完成之後**公開金鑰**角色擁有`CONNECT`以外的所有端點上的權限**Dedicated Admin Connection**。 這是正常狀況，通常不應該變更 (存取控制使用`CONNECT SQL`建立新的登入時自動授與的權限。)  
  
### <a name="for-more-information"></a>如需詳細資訊  
 [保護 SQL Server 的安全](../security/securing-sql-server.md)  
  
  
