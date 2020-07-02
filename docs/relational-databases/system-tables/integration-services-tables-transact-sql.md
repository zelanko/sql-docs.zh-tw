---
title: Integration Services 資料表（Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Integration Services system tables
- system tables [SQL Server], Integration Services
- system tables [Integration Services]
- SSIS, system tables
ms.assetid: 683b181b-0091-4a9c-86db-bc577af43cec
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c341ae73981eb0d06a2a1e64e804db9f81297fdd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773748"
---
# <a name="integration-services-tables-transact-sql"></a>Integration Services 資料表 (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  本節中的主題描述 msdb 資料庫中儲存所使用之資訊的系統資料表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 。  
  
## <a name="in-this-section"></a>本節內容  
 [sysssislog](../../relational-databases/system-tables/sysssislog-transact-sql.md)  
 針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝在執行階段產生的每個記錄項目，各包含一個資料列。  
  
 只有當封裝使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄提供者時，才會使用這個資料表。  
  
 [sysssispackagefolders](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md)  
 針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務用來組織封裝的每個邏輯資料夾，各包含一個資料列。 資料行值會定義巢狀資料夾之間的父子式關聯性。  
  
> [!NOTE]  
>  當您連接至 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 服務時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 就會以階層式檢視顯示儲存的封裝。  
  
 [sysssispackages](../../relational-databases/system-tables/sysssispackages-transact-sql.md)  
 針對每個 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，各包含一個資料列。  
  
 只有當您將封裝儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，才會使用這個資料表。  
  
  
