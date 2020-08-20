---
description: 壓縮資料庫工作
title: 壓縮資料庫工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.shrinkdatabasetask.f1
helpviewer_keywords:
- Shrink Database task
- database shrinking [Integration Services]
- shrinking databases
ms.assetid: e66286f8-97b1-4e5a-86b4-e56f1932b7d5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 066a41ecdb41ff27d0043204c6254b65371e6b15
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495969"
---
# <a name="shrink-database-task"></a>壓縮資料庫工作

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  「壓縮資料庫」工作會減少 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫資料和記錄檔的大小。  
  
 藉由使用「壓縮資料庫」工作，封裝可壓縮單一資料庫或多重資料庫的檔案。  
  
 將資料頁面從檔案結尾移到靠近檔案前端的未使用空間，以壓縮資料並復原儲存空間。 當檔案結尾建立了足夠的可用空間後，檔案結尾的資料頁面便可取消配置並返回檔案系統。  
  
> [!WARNING]  
>  為壓縮檔案所移動的資料可散佈至檔案中的任何可用位置。 如此會造成索引片段，並可能導致大範圍之索引搜尋的查詢效能變慢。 若要消除資料片段，可考慮在壓縮之後重建該檔案的索引。  
  
## <a name="commands"></a>命令  
 「壓縮資料庫」工作會封裝 DBCC SHRINKDATABASE 命令，包括下列引數和選項：  
  
-   *database_name*  
  
-   *target_percent*  
  
-   NOTRUNCATE 或 TRUNCATEONLY。  
  
 如果「壓縮資料庫」工作壓縮多個資料庫，則工作會執行多個 SHRINKDATABASE 命令，亦即針對每個資料庫執行一個命令。 SHRINKDATABASE 命令的所有執行個體會使用相同的引數值，但 *database_name* 引數例外。 如需詳細資訊，請參閱 [DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
## <a name="configuration-of-the-shrink-database-task"></a>壓縮資料庫工作的組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師設定屬性。 這項工作位於「 **設計師」中** [工具箱] **的** [維護計畫工作] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 區段。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列主題：  
  
-   [壓縮資料庫工作 &#40;維護計畫&#41;](../../relational-databases/maintenance-plans/shrink-database-task-maintenance-plan.md)  
  
 如需有關在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  
