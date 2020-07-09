---
title: 維護計畫 (管理連接) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.connections.f1
ms.assetid: 95ad9375-6584-423e-b9de-0e86782f8017
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 495ec4a69d960cfec8534b37490b10fe66c5934d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754541"
---
# <a name="maintenance-plan-manage-connections"></a>維護計畫 (管理連接)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  使用 **[管理連接]** 對話方塊，來指定維護計畫所用的連接屬性。 建立維護計畫時，會在建立此計畫的伺服器建立本機連接。 使用此連接即可建立工作 (Task)，在本機連接上執行工作 (Work)。 需要時，請使用 **[管理連接]** 對話方塊將它們加入。 設定其他連接時，它們會出現在每個工作的連接方塊中。  
  
## <a name="options"></a>選項。  
 **Server**  
 伺服器執行個體。  
  
 **驗證**  
 指出是以 Windows 驗證或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來建立連接。  

> [!IMPORTANT]  
> 套件會儲存在 **msdb** 資料庫中，且將 **ProtectionLevel** 設為 **ServerStorage**，因此在使用「SQL Server 驗證」  時，**msdb** 中的密碼將不會加密。 只要 **msdb** 是安全的，您就可以使用「SQL Server 驗證」，但建議使用「Windows 驗證」

## <a name="see-also"></a>另請參閱  
 [維護計畫](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
  
