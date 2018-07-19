---
title: 自主資料庫與 AlwaysOn 可用性群組 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- contained database [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: cacce3ae-e940-4566-8298-6607c4268e74
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5086a557319d4db305f4a3d5d6c2df6437e3f8c1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37285704"
---
# <a name="contained-databases-with-always-on-availability-groups-sql-server"></a>自主資料庫與 AlwaysOn 可用性群組 (SQL Server)
  本主題包含在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 中使用自主資料庫搭配 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]的相關資訊。  
  
 **本主題內容：**  
  
-   [必要條件](#Prerequisites)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="Prerequisites"></a> 必要條件  
  
-   將自主資料庫加入至可用性群組之前，請確定在裝載可用性群組之可用性複本的每個伺服器執行個體上，`contained database authentication` 伺服器選項都設為 `1`。 如需詳細資訊，請參閱 [自主資料庫驗證伺服器組態選項](../../configure-windows/contained-database-authentication-server-configuration-option.md) 和 [伺服器組態選項 &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)的相關資訊。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [伺服器組態選項 &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [自主資料庫](../../../relational-databases/databases/contained-databases.md)  
  
  
