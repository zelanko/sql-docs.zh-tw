---
title: 伺服器 public 權限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a0b125841e2d3c9f03b7ba46519f80af9293a1cd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035197"
---
# <a name="server-public-permissions"></a>伺服器 public 權限
  此規則會判斷 public 伺服器角色是否有伺服器權限。 伺服器上建立的每一個登入都是 public 伺服器角色的成員。 如果符合這個條件，伺服器上的每個登入都具有伺服器權限。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 請勿將伺服器權限授與給伺服器 public 角色。  
  
> [!IMPORTANT]  
>  安裝程式完成之後**公用**角色有`CONNECT`權限以外的所有端點**Dedicated Admin Connection**。 這是正常狀況，通常不應該變更 (存取控制使用`CONNECT SQL`建立新的登入時自動授與權限。)  
  
### <a name="for-more-information"></a>如需詳細資訊  
 [保護 SQL Server 的安全](../security/securing-sql-server.md)  
  
  