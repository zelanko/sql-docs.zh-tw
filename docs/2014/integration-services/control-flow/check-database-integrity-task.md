---
title: 檢查資料庫完整性工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.checkdatabaseintegritytask.f1
helpviewer_keywords:
- data integrity [Integration Services]
- Check Database Integrity task [Integration Services]
- checking database consistency
- database consistency checks [Integration Services]
- verifying database consistency
- integrity checking [Integration Services]
ms.assetid: 5a82fe99-4503-429f-9337-e6bac7649fe4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a123557bdeb84ed8d36664b6451772b669edbbec
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375316"
---
# <a name="check-database-integrity-task"></a>檢查資料庫完整性工作
  「檢查資料庫完整性」工作會檢查指定資料庫中所有物件的配置及結構完整性。 這項工作可檢查單一資料庫或多個資料庫，而且您可以選擇是否同時檢查資料庫索引。  
  
 「檢查資料庫完整性」工作會封裝 DBCC CHECKDB 陳述式。 如需詳細資訊，請參閱 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)。  
  
## <a name="configuration-of-the-check-database-integrity-task"></a>設定檢查資料庫完整性工作  
 您可以透過 [ [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師] 設定屬性。 這項工作位於「 **設計師」中** [工具箱] **的** [維護計畫工作] [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 區段。  
  
 如需有關可在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列主題：  
  
-   [檢查資料庫完整性工作 &#40;維護計畫&#41;](../../relational-databases/maintenance-plans/check-database-integrity-task-maintenance-plan.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
  
