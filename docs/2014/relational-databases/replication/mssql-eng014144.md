---
title: MSSQL_ENG014144 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014144 error
ms.assetid: fdc744d5-530e-48c4-9420-cca032fd482b
caps.latest.revision: 11
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7e4d3991806fe3f2275fd94f3ffbacc1c94ccbd8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133177"
---
# <a name="mssqleng014144"></a>MSSQL_ENG014144
    
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
  
1.  在「發行者」端的發行集資料庫中執行 [sp_helpsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql) 以尋找訂閱。  
  
2.  在發行集資料庫中執行 [sp_dropsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql) 以卸除訂閱。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)   
 [訂閱發行集](subscribe-to-publications.md)  
  
  
