---
title: 重建索引工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rebuildindextask.f1
helpviewer_keywords:
- rebuilding indexes
- indexes [Integration Services]
- Rebuild Index task
ms.assetid: 021884dd-e72d-47b2-99e8-b741410509c3
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 509c45f7c1efc0e7fff3b1567aa02a1a6fcecacc
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35410080"
---
# <a name="rebuild-index-task"></a>重建索引工作
  「重建索引」工作會重建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫資料表與檢視中的索引。 如需管理索引的詳細資訊，請參閱 [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
 藉由使用「重建索引」工作，封裝可重建單一資料庫或多重資料庫中的索引。 如果此工作只重建單一資料庫中的索引，您可以選擇要由此工作重建索引的檢視與資料表。  
  
 此工作使用下列索引重建選項封裝 ALTER INDEX REBUILD 陳述式：  
  
-   指定 FILLFACTOR 百分比或使用原始 FILLFACTOR 數量。  
  
-   設定 SORT_IN_TEMPDB = ON，將用來重建索引的中繼排序結果儲存在 tempdb 中。 當中繼排序結果設為 OFF 時，結果會與索引儲存在相同資料庫中。  
  
-   設定 PAD_INDEX = ON，將 FILLFACTOR 所指定的可用空間配置給中級索引分頁。  
  
-   設定 IGNORE_DUP_KEY = ON，允許包含違反唯一條件約束之記錄的多資料列插入作業，以插入不違反唯一條件約束的記錄。  
  
-   設定 ONLINE = ON，不要持有資料表鎖定，以便對基礎資料表的查詢或更新可在重建索引期間繼續進行。  
  
    > [!NOTE]  
    >  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有版本都無法使用線上索引作業。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
-   請指定 MAXDOP 值來限制執行平行計畫所用的處理器數目。  
  
-   指定 WAIT_AT_LOW_PRIORITY、MAX_DURATION 及 ABORT_AFTER_WAIT，控制索引作業等候低優先權鎖定的時間長度。  
  
 如需 ALTER INDEX 陳述式和索引重建選項的詳細資訊，請參閱 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)。  
  
> [!IMPORTANT]  
>  此工作用於建立工作執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式之時間，與工作重建的索引數目成正比。 如果此工作設定成重建含有大量索引的資料庫內所有資料表與檢視中的索引，或是重建多重資料庫中的索引，則此工作可能會花費相當多的時間產生 Transact-SQL 陳述式。  
  
## <a name="configuration-of-the-rebuild-index-task"></a>設定重建索引工作  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」設定屬性 這項工作位於「 **設計師」中** [工具箱] **的** [維護計畫工作] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 區段。  
  
 如需有關可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列主題：  
  
 [重建索引工作 &#40;維護計畫&#41;](../../relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具中設定這些屬性的詳細資訊，請參閱 [Set the Properties of a Task or Container](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)(設定工作或容器的屬性)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
