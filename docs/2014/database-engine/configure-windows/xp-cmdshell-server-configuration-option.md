---
title: xp_cmdshell 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9f4ab373c9827adff6e0138a81b5eaa57d1c4414
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/30/2018
ms.locfileid: "52639436"
---
# <a name="xpcmdshell-server-configuration-option"></a>xp_cmdshell 伺服器組態選項
  **xp_cmdshell** 選項是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器組態選項，可讓系統管理員控制 **xp_cmdshell** 擴充預存程序是否可在系統上執行。 根據預設， **xp_cmdshell** 選項會在新安裝上停用，而且可以使用原則式管理或執行 **sp_configure** 系統預存程序來啟用，如下列程式碼範例所示：  
  
```  
-- To allow advanced options to be changed.  
EXEC sp_configure 'show advanced options', 1;  
GO  
-- To update the currently configured value for advanced options.  
RECONFIGURE;  
GO  
-- To enable the feature.  
EXEC sp_configure 'xp_cmdshell', 1;  
GO  
-- To update the currently configured value for this feature.  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [使用原則式管理來管理伺服器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
