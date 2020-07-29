---
title: 設定錯誤記錄檔 (一般頁面)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.errorlog.configure.f1
ms.assetid: e08de622-6f87-470c-aee0-b2d6cb6cca88
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6e23a0c27675a9d873387dc2face6924d7541fdc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749121"
---
# <a name="configure-sql-server-agent-error-logs-general-page"></a>設定 SQL Server Agent 錯誤記錄檔 (一般頁面)

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此畫面來檢視和更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 錯誤記錄的設定。  
  
## <a name="options"></a>選項。  
**錯誤記錄檔**  
指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 要將錯誤記錄檔寫入的檔案。  
  
**...**  
瀏覽錯誤記錄檔。  
  
**寫入 OEM 錯誤記錄檔**  
將錯誤記錄檔寫成非 Unicode 檔案。 如此可減少記錄檔所用的磁碟空間大小。 不過，啟用此選項時，可能更難以讀取包含 Unicode 資料的訊息。  
  
**錯誤**  
只將錯誤和參考用訊息寫入記錄檔。  
  
**警告**  
只將警告和參考用訊息寫入記錄檔。  
  
**資訊**  
只將參考用訊息寫入記錄檔。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server Agent 錯誤記錄檔](../../ssms/agent/sql-server-agent-error-log.md)  
  
