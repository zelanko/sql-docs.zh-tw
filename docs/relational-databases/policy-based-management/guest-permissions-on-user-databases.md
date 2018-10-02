---
title: 使用者資料庫的 Guest 權限 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 540f1c6d-df51-497e-958a-3a0f429d2920
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 366ee3f80bacbd1cf17bcec7ed0c4e04ce892277
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787976"
---
# <a name="guest-permissions-on-user-databases"></a>使用者資料庫的 Guest 權限
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此規則會判斷 guest 使用者是否有權存取資料庫。 此規則只適用於使用者資料庫。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 撤銷 guest 使用者存取資料庫的權限 (如果不需要的話)。  
  
 雖然您不能卸除 guest 使用者，但是可以在 master、tempdb 或 msdb 以外的任何資料庫中執行 REVOKE CONNECT FROM GUEST 來撤銷其 CONNECT 權限，以停用 guest 使用者。  
  
## <a name="for-more-information"></a>詳細資訊  
 [保護 SQL Server 的安全](../../relational-databases/security/securing-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
