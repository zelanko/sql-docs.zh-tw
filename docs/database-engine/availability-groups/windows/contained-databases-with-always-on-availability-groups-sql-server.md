---
title: 搭配使用自主資料庫與可用性群組
description: 如何搭配使用自主資料庫與 Always On 可用性群組
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- contained database, AlwaysOnAvailabilityGroups
ms.assetid: cacce3ae-e940-4566-8298-6607c4268e74
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: b93c4c91051284a944e3b234da3f4523b3092623
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66793548"
---
# <a name="use-contained-databases-with-always-on-availability-groups"></a>搭配使用自主資料庫與 AlwaysOn 可用性群組 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主題包含在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 中使用自主資料庫搭配 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]的相關資訊。  
  
##  <a name="Prerequisites"></a> 必要條件  
  
-   在可用性群組中加入自主資料庫之前，請確定在裝載可用性群組之可用性複本的每個伺服器執行個體上， **自主資料庫驗證** 伺服器選項都設為 **1** 。 如需詳細資訊，請參閱 [自主資料庫驗證伺服器組態選項](../../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md) 和 [伺服器組態選項 &#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)的相關資訊。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [伺服器組態選項 &#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [自主資料庫](../../../relational-databases/databases/contained-databases.md)  
  
  
