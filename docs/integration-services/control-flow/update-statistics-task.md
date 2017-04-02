---
title: "更新統計資料工作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.updatestatisticstask.f1"
helpviewer_keywords: 
  - "更新統計資料"
  - "更新統計資料工作 [Integration Services]"
ms.assetid: 0247483b-f092-4511-8fa8-3610108bd1bc
caps.latest.revision: 45
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 45
---
# 更新統計資料工作
  「更新統計資料」工作會在指定的資料表或索引檢視表中，更新一個或多個統計群組 (集合) 索引鍵值散發的詳細資訊。 如需詳細資訊，請參閱 [Statistics](../../relational-databases/statistics/statistics.md)。  
  
 藉由使用「更新統計資料」工作，封裝可更新單一資料庫或多重資料庫的統計資料。 如果此工作只更新單一資料庫中的統計資料，您可以選擇要由此工作更新統計資料的檢視或資料表。 您可以將更新作業設定為更新所有統計資料、只更新資料行統計資料，或只更新索引統計資料。  
  
 此工作會封裝 UPDATE STATISTICS 陳述式，包括下列引數和子句在內：  
  
-   *table_name* 或 *view_name* 引數。  
  
-   如果更新套用至所有統計資料，則會隱含 WITH ALL 子句。  
  
-   如果更新只套用至資料行，則會包含 WITH COLUMN 子句。  
  
-   如果更新只套用至索引，則會包含 WITH INDEX 子句。  
  
 如果「更新統計資料」工作更新多重資料庫中的統計資料，則此工作會執行多個 UPDATE STATISTICS 陳述式，每個資料表或檢視各一個。 UPDATE STATISTICS 的所有執行個體都使用相同的子句，但使用不同的 *table_name* 或 *view_name* 值。 如需詳細資訊，請參閱 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md) 和 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)。  
  
> [!IMPORTANT]  
>  此工作用於建立工作執行的 Transact-SQL 陳述式之時間，與工作更新的統計資料數成正比。 如果此工作設定成更新含有大量索引的資料庫內所有資料表與檢視表中的統計資料，或是更新多重資料庫中的統計資料，則此工作可能會花費相當多的時間產生 Transact-SQL 陳述式。  
  
## 設定更新統計資料工作  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」設定屬性 這項工作位於「 **設計師」中** [工具箱] **的** [維護計畫工作] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 區段。  
  
 如需有關可在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列主題：  
  
-   [更新統計資料工作 &#40;維護計畫&#41;](../../relational-databases/maintenance-plans/update-statistics-task-maintenance-plan.md)  
  
## 相關工作  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## 請參閱＜  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
  