---
description: 設定 CPU 閒置時間與期間
title: 設定 CPU 閒置時間與期間
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CPU [SQL Server], idle conditions
- time [SQL Server], CPU idle and duration
- duration of CPU idle [SQL Server]
- SQL Server Agent, CPU idle conditions
- idle time [SQL Server]
ms.assetid: 8647b465-d899-4cc7-9640-134a506d0a2e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 75670401aa4049c66083f0dce5bf4212e4f74f5f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418074"
---
# <a name="set-cpu-idle-time-and-duration"></a>設定 CPU 閒置時間與期間

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主題說明如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]定義伺服器的 CPU 閒置條件。 CPU 閒置定義會影響 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 回應事件的方式。 例如，假設您將 CPU 閒置條件定義為平均 CPU 使用量低於百分之十且此狀態持續 10 分鐘。 然後，如果您已定義每當伺服器 CPU 達到閒置條件時要執行的作業，當 CPU 使用量低於百分之十且此狀態持續 10 分鐘，將會執行該作業。 如果此作業會明顯影響伺服器的效能，則如何定義 CPU 閒置條件就很重要。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-set-cpu-idle-time-and-duration"></a>若要設定 CPU 閒置時間與期間  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]****，按一下 [屬性]****，然後選取 [進階]**** 頁面。  
  
3.  在 **[閒置 CPU 的條件]** 下方，執行下列步驟：  
  
    -   核取 **[定義閒置 CPU 的條件]**。  
  
    -   在 [平均 CPU 使用量低於]**** \(所有 CPU) 方塊中指定百分比。 這樣會設定 CPU 必須低於此使用量才會視為閒置。  
  
    -   在 **[並且持續低於此狀態達]** 方塊中指定秒數。 這樣會設定此期間必須維持最小 CPU 用量才會視為閒置。  
  
