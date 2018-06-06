---
title: MSSQL_ENG014144 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014144 error
ms.assetid: fdc744d5-530e-48c4-9420-cca032fd482b
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f88a127741e42fef78d6acb596427a7fd6081621
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="mssqleng014144"></a>MSSQL_ENG014144
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|14144|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|無法卸除訂閱者 '%s'。 發行集資料庫 '%s' 中有其訂閱。|  
  
## <a name="explanation"></a>說明  
 如果存在為執行個體設定的使用中訂閱，則設定為「訂閱者」的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體將無法從「訂閱者」角色中移除。  
  
## <a name="user-action"></a>使用者動作  
 在嘗試變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的「訂閱者」狀態之前，請先卸除所有相關聯的訂閱。  
  
1.  在「發行者」端的發行集資料庫中執行 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) 以尋找訂閱。  
  
2.  在發行集資料庫中執行 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md) 以卸除訂閱。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
