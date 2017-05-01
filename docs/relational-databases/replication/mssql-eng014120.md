---
title: MSSQL_ENG014120 | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014120 error
ms.assetid: 6b169a3b-30da-4981-b998-b52d61811572
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 127a8b4b7b1b91559ad221e38eff2475b34b3ddf
ms.lasthandoff: 04/11/2017

---
# <a name="mssqleng014120"></a>MSSQL_ENG014120
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|14120|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|無法卸除散發資料庫 '%s'。 這個散發資料庫與一發行者相關聯。|  
  
## <a name="explanation"></a>說明  
 散發資料庫為異動複寫中所有類型的複寫與交易，儲存中繼資料和歷程資料。 若您嘗試卸除與一個或多個發行者相關聯的散發資料庫，就會發生這個錯誤。  
  
## <a name="user-action"></a>使用者動作  
 若要卸除散發資料庫，您必須先卸除「散發者」與「發行者」之間的關聯。 如需詳細資訊，請參閱 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [設定散發](../../relational-databases/replication/configure-distribution.md)  
  
  
