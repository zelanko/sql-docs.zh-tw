---
title: 重大變更至 管理工具 SQL Server 2014 中的功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3ff3fad8-b569-4516-bd58-5a3efeb537e2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f206da123659c750f955d2132142dcae76df6a46
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165349"
---
# <a name="breaking-changes-to-management-tools-features-in-sql-server-2014"></a>SQL Server 2014 中管理工具功能的突破性變更
  此主題描述管理工具功能的突破性變更。 這些變更可能會中斷以舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]為根據的應用程式、指令碼或功能。 當您升級時可能會遇到這些問題。 如需詳細資訊，請參閱＜ [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)＞。  
  
## <a name="breaking-changes-in-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 的最新變更  
 將於日後提供資訊。  
  
## <a name="breaking-changes-in-includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 的最新變更  
  
### <a name="you-cannot-use-includesssql11includessssql11-mdmd-management-tools-to-create-a-utility-control-point-on-a-includesskilimanjaroincludessskilimanjaro-mdmd-instance-of-sql-server"></a>您無法在 SQL Server 的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 執行個體上，使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 管理工具建立公用程式控制點。  
 若要在 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]的執行個體上建立公用程式控制點，請使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 管理工具。  
  
### <a name="smo-has-been-reversioned-in-includesssql11includessssql11-mdmd"></a>SMO 已經在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 或更早版本的 SMO 所開發的程式碼必須稍微修改，才能針對 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 進行建立。 如需詳細資訊，請參閱 [Backward Compatibility in SMO](../relational-databases/server-management-objects-smo/backward-compatibility-in-smo.md)。  
  
## <a name="see-also"></a>另請參閱  
 [回溯相容性](../../2014/getting-started/backward-compatibility.md)  
  
  
