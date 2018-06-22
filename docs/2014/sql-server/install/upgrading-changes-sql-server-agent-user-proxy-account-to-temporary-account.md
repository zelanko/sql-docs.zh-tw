---
title: 升級會將 SQL Server Agent 使用者 Proxy 帳戶變更為暫時的 upgradedproxyaccount |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- log shipping [SQL Server Agent]
ms.assetid: cd2d08c3-4e56-4034-8b68-0c78df8b5471
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9bae867b97a9fc63b97506fd8900e68b670b8013
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023025"
---
# <a name="upgrading-will-change-the-sql-server-agent-user-proxy-account-to-the-temporary-upgradedproxyaccount"></a>升級會將 SQL Server Agent 使用者 Proxy 帳戶變更為暫時的 UpgradedProxyAccount
  升級之後，已啟用記錄傳送的資料庫維護計劃將無法啟用。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>描述  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供一組與資料庫維護計劃不直接相容的新記錄傳送功能。  
  
## <a name="corrective-action"></a>更正動作  
 擁有包含記錄傳送功能之資料庫維護計劃的 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 使用者應該使用新的功能來設定記錄傳送。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜記錄傳送＞。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 記錄傳送作業類別目錄會造成升級失敗](../../../2014/sql-server/install/sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail.md)   
 [在升級之後將不會執行記錄傳送](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)  
  
  