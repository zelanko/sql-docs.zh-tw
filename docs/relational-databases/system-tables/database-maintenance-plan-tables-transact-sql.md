---
title: 資料庫維護計畫資料表 (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- database maintenance plans [SQL Server]
- maintenance plans [SQL Server], system tables
- system tables [SQL Server], database maintenance plans
ms.assetid: f264554c-5514-4df2-aadb-6dcdc2dfcfea
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc48ab97d774583f9a9e25edd2cc55c9f2758957
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="database-maintenance-plan-tables-transact-sql"></a>資料庫維護計畫資料表 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  此章節的主題介紹儲存資料庫維護計畫所用的資訊之系統資料表。 這些資料表會保留從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級而來之執行個體的資訊。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
## <a name="in-this-section"></a>本節內容  
 [sysdbmaintplan_databases](../../relational-databases/system-tables/sysdbmaintplan-databases-transact-sql.md)  
 針對每個有相關升級之資料庫維護計畫的資料庫，各包含一個資料列。  
  
 [sysdbmaintplan_history](../../relational-databases/system-tables/sysdbmaintplan-history-transact-sql.md)  
 針對每個所執行之升級的資料庫維護計畫動作，各包含一個資料列。  
  
 [sysdbmaintplan_jobs](../../relational-databases/system-tables/sysdbmaintplan-jobs-transact-sql.md)  
 針對每個升級的資料庫維護計畫作業，各包含一個資料列。  
  
 [sysdbmaintplans](../../relational-databases/system-tables/sysdbmaintplans-transact-sql.md)  
 針對每個升級的資料庫維護計畫，各包含一個資料列。  
  
## <a name="see-also"></a>另請參閱  
 [中 [物件總管] 之](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
  
