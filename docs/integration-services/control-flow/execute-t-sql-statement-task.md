---
title: 執行 T-SQL 陳述式工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executetsqlstatementtask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- Execute T-SQL Statement task [Integration Services]
ms.assetid: 7e9086ca-d27e-46c0-bfad-d61333ebd55e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0e7b51e71feef1dcd30b3e63c38b6cf10598cd80
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71294164"
---
# <a name="execute-t-sql-statement-task"></a>執行 T-SQL 陳述式工作

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  「執行 T-SQL 陳述式」工作會執行 Transact-SQL 陳述式。 如需詳細資訊，請參閱 [Transact-SQL 參考 &#40;資料庫引擎&#41;](../../t-sql/transact-sql-reference-database-engine.md) 和 [Integration Services &#40;SSIS&#41; 查詢](../../integration-services/integration-services-ssis-queries.md)。  
  
 此工作與執行 SQL 工作類似。 不過，「執行 T-SQL 陳述式」工作僅支援 Transact-SQL 版的 SQL 語言，而且您無法在使用其他 SQL 語言方言的伺服器上使用此工作執行陳述式。 如果您需要執行參數化查詢、將查詢結果儲存至變數，或使用屬性運算式，則應使用執行 SQL 工作而非「執行 T-SQL 陳述式」工作。 如需相關資訊，請參閱 [Execute SQL Task](../../integration-services/control-flow/execute-sql-task.md)。  
  
## <a name="configuration-of-the-execute-t-sql-task"></a>設定執行 T-SQL 工作  
 您可以透過 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 設定屬性。 這項工作位於「 **設計師」中** [工具箱] **的** [維護計畫工作] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 區段。  
  
 如需有關可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列主題：  
  
-   [執行 T-SQL 陳述式工作 &#40;維護計畫&#41;](../../relational-databases/maintenance-plans/execute-t-sql-statement-task-maintenance-plan.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)   
 [Integration Services 套件中的 MERGE](../../integration-services/control-flow/merge-in-integration-services-packages.md)  
  
  
