---
title: 修改邊緣條件約束 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- alter edge constraints
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e5b6a471156f0b1371c727ce96aac72f4f812dac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62693315"
---
# <a name="modify-edge-constraints"></a>修改邊緣條件約束
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]，在 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] 中修改邊緣條件約束。 您可以變更邊緣條件約束子句順序或新增子句，以修改邊緣資料表的邊緣條件約束。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要修改邊緣條件約束，請使用：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料表的 ALTER 權限。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL
 若要使用 Transact-SQL 來修改邊緣條件約束，您必須先刪除現有的邊緣條件約束，然後使用新的定義來重新建立。 如需詳細資訊，請參閱[刪除邊緣條件約束](../../relational-databases/tables/delete-edge-constraint.md)和[建立邊緣條件約束](../../relational-databases/tables/create-edge-constraints.md)。    
 
