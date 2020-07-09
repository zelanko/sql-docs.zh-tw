---
title: MSSQL_ENG003724 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG003724 error
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: d692345d5403c805369e8e415863131623694779
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85721959"
---
# <a name="mssql_eng003724"></a>MSSQL_ENG003724
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|3724|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|無法 %S_MSG %S_MSG '%.*ls'，因為它正用於複寫。|  
  
## <a name="explanation"></a>說明  
 複寫資料庫中的物件時，會在系統資料表 **sysarticles** (適用快照集和交易式發行集) 或 **sysmergearticles** (適用合併發行集) 中將它們標記為已複寫。 如果您嘗試放入已複寫物件，便會發生這個錯誤。  
  
## <a name="user-action"></a>使用者動作  
 在放入資料庫物件之前，請先確定它並未複寫。 例如：  
  
-   如果在發行集資料庫中發生錯誤，請在放入該物件之前先從發行集中放入發行項。 如需詳細資訊，請參閱[在現有發行集中新增和卸除發行項](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
-   如果在訂閱資料庫中發生錯誤，請在放入該物件之前先放入訂閱。 如需詳細資訊，請參閱[訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)。 針對交易式發行集的訂閱，可以將訂閱放入個別發行項，而非整個發行集。 如需詳細資訊，請參閱 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)。  
  
 如果在未複寫的資料庫中發生這個錯誤，請執行 [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)，以確保資料庫中的物件不會標示為已複寫。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
