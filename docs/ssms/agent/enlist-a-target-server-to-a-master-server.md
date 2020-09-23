---
description: 將目標伺服器編列至主要伺服器
title: 將目標伺服器編列至主要伺服器
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b75aca103c33ff30a2f524c511420e79b7e01a7f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480409"
---
# <a name="enlist-a-target-server-to-a-master-server"></a>將目標伺服器編列至主要伺服器
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何將目標伺服器新增至多伺服器管理組態。 從主要伺服器執行這個程序。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]或 SQL Server 管理物件 (SMO)。  
  
如需有關用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務之 Windows 帳戶如何影響多伺服器環境的詳細資訊，請參閱 [建立多伺服器環境](../../ssms/agent/create-a-multiserver-environment.md)。  
  
根據預設，主要伺服器與目標伺服器之間的連線會啟用完整「傳輸層安全性」(TLS) (先前稱為「安全通訊端層」(SSL)) 加密和憑證驗證。 如需詳細資訊，請參閱 [在目標伺服器上設定加密選項](../../ssms/agent/set-encryption-options-on-target-servers.md)。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-enlist-a-target-server"></a>若要編列目標伺服器  
  
1.  在 **[物件總管]** 中，展開設定為主要伺服器的伺服器。  
  
2.  以滑鼠右鍵按一下 **[SQL Server Agent]** ，指向 **[多伺服器管理]** ，然後按一下 **[新增目標伺服器]** 。  
  
3.  完成「目標伺服器精靈」，精靈將引導您完成此程序。  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-enlist-a-target-server"></a>若要編列目標伺服器  
  
1.  **sp_msx_enlist** 預存程序會編輯登錄。  如需詳細資訊，請參閱 [sp_msx_enlist (Transact-SQL)](https://msdn.microsoft.com/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)  
  
## <a name="see-also"></a>另請參閱  
[將整個企業的管理自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
