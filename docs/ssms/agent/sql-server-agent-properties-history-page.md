---
description: SQL Server Agent 屬性 (記錄頁面)
title: SQL Server Agent 屬性 (記錄頁面)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ecc35e03cef1a6c139fc1bf3d848e82433a01a5d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480293"
---
# <a name="sql-server-agent-properties-history-page"></a>SQL Server Agent 屬性 (記錄頁面)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此頁面來檢視和修改 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務記錄的管理設定。  
  
## <a name="options"></a>選項  
**限制作業記錄大小**  
對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 在記錄中所保留的作業記錄資訊量加以設限。  
  
**作業記錄大小上限 (以資料列為單位)**  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會保留的最大資料列數目。 當記錄成長至此資料列數目時，隨著新資料列的輸入， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會移除記錄中最舊的資料列。  
  
**每項作業的作業記錄最大資料列數**  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會為每項作業保留的最大資料列數目。 當特定作業的記錄成長至此資料列數目時，隨著新資料列的輸入， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會移除記錄中最舊的資料列。  
  
**移除代理程式記錄**  
指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會移除已存在於記錄中超過指定時間長度的項目。 這是單次移除記錄的執行作業。 如果需要重複的作業，請建立並排程含有清除作業的維護計畫。  
  
**早於**  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會保留項目的時間。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server Agent 錯誤記錄檔](../../ssms/agent/sql-server-agent-error-log.md)  
  
