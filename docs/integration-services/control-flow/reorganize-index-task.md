---
title: "重新組織索引工作 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.reorganizeindextask.f1
helpviewer_keywords:
- reorganizing indexes
- Reorganize Index task [Integration Services]
- indexes [Integration Services]
ms.assetid: 9ed87861-e5c3-4fcd-8760-d112f4c0af0c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac9472f57a4f5c2ecf8cbcb7895b960531b62ca1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="reorganize-index-task"></a>重新組織索引工作
  「重新組織索引」工作會重新組織 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫資料表與檢視中的索引。 如需管理索引的詳細資訊，請參閱 [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
 藉由使用「重新組織索引」工作，封裝可重新組織單一資料庫或多重資料庫中的索引。 如果此工作只重新組織單一資料庫中的索引，您可以選擇要由此工作重新組織索引的檢視或資料表。 「重新組織索引」工作亦包含壓縮大型物件資料的選項。 大型物件資料是指 **image**、**text**、**ntext**、**varchar(max)**、**nvarchar(max)**、**varbinary(max)** 或 **xml** 資料類型的資料。 如需詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。  
  
 「重新組織索引」工作封裝 Transact-SQL ALTER INDEX 陳述式。 如果您選擇壓縮大型物件資料，陳述式便會使用 REORGANIZE WITH (LOB_COMPACTION = ON) 子句，否則 LOB_COMPACTION 會設為 OFF。 如需詳細資訊，請參閱 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)。  
  
> [!IMPORTANT]  
>  此工作用於建立工作執行的 Transact-SQL 陳述式之時間，與工作重新組織的索引數目成正比。 如果工作設定成重新組織擁有大量索引的資料庫內所有資料表與檢視中的索引，或是重新組織多重資料庫中的索引，則此工作可能會花費相當多的時間產生 Transact-SQL 陳述式。  
  
## <a name="configuration-of-the-reorganize-index-task"></a>重新組織索引工作的組態  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」設定屬性 這項工作位於「 **設計師」中** [工具箱] **的** [維護計畫工作] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 區段。  
  
 如需有關可在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列主題：  
  
-   [重新組織索引工作 &#40;維護計畫&#41;](../../relational-databases/maintenance-plans/reorganize-index-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定這些屬性的詳細資訊，請參閱 [設定工作或容器的屬性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  
