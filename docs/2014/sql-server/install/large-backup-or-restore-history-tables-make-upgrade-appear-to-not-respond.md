---
title: 大型備份或還原記錄資料表會使升級作業看似無回應 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backup history tables
- history tables
ms.assetid: f88d86ec-324b-4518-b6d7-1af7e7265812
caps.latest.revision: 21
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d01d73f9456d56a8f12698b954213289ab4921d7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208498"
---
# <a name="large-backup-or-restore-history-tables-make-upgrade-appear-to-not-respond"></a>大型備份或還原記錄資料表會使升級作業看似沒有回應
  在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，新的資料行會加入至某些備份和還原記錄資料表。 升級這些資料表需要更改它們，以便加入新的資料行。 如果其中一個或多個資料表包含大量資料列，則升級會延滯相當長的一段時間，等候 ALTER TABLE 陳述式將資料行加入至該資料表。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 如果下列任何備份或還原記錄資料表包含大量資料列，升級作業可能會看似已停止回應：  
  
-   **backupfile**  
  
-   **backupmediafamily**  
  
-   **backupmediaset**  
  
-   **backupset**  
  
-   **restorefile**  
  
-   **restorefilegroup**  
  
-   **restorehistory**  
  
 如果其中任何資料表含有 10,000 個以上的資料列，Upgrade Advisor 會報告不相容的失敗。 但是，它不會報告哪一份資料表超過允許的資料列數目。 超過 10,000 個資料列的第一份資料表會導致失敗。  
  
## <a name="corrective-action"></a>更正動作  
 升級資料庫之前，如果其中任何資料表超過 10,000 個資料列，我們建議您將此數目縮減為小於 10,000。 若要縮減所有這些資料表中的資料列，您可以執行**sp_delete_backuphistory**預存程序。 這個程序會在所有備份和還原記錄資料表中刪除早於指定日期之備份組的項目。 如需詳細資訊，請參閱 [sp_delete_backuphistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql)。  
  
> [!NOTE]  
>  您可以升級備份和還原記錄資料表大於 10,000 個資料列的資料庫。 但是當系統更改大型資料表時，升級作業可能會看似延滯。 資料表的體積越大，安裝程式完成作業所花費的時間就越長。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
