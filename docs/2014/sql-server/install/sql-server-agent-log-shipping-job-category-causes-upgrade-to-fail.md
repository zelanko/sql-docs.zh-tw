---
title: SQL Server Agent 記錄傳送作業類別目錄會導致升級失敗 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server Agent]
- job categories [SQL Server Agent]
ms.assetid: ef05ce53-c6ce-42ec-9df8-46c951626424
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7145d846657613b50706ebe75c9832f40f49383e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092034"
---
# <a name="sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail"></a>SQL Server Agent 記錄傳送作業類別目錄會造成升級失敗
  如果您目前存在名為「記錄傳送」的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式作業類別，升級程序將會失敗。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>描述  
 有名為「記錄傳送」的系統作業類別。 如果正在升級的安裝已經包含名為「記錄傳送」的使用者建立作業類別目錄，您就必須重新命名此作業類別目錄，然後再升級。否則，升級程序將會失敗。  
  
## <a name="see-also"></a>另請參閱  
 [升級後將不會執行記錄傳送](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)   
 [升級會將 SQL Server Agent 的使用者 Proxy 帳戶變更為暫時的 UpgradedProxyAccount](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [SQL Server Agent 升級問題](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
