---
title: 微調企業整體的自動化管理 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- performance [SQL Server], automated administration
- tuning automated administration [SQL Server]
- monitoring performance [SQL Server], automated administration
ms.assetid: 671fed35-3859-4b0d-8f38-4dd07436857e
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1df873096698a1101fadf401904b9cefb367b9a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65089334"
---
# <a name="tune-automated-administration-across-an-enterprise"></a>微調企業整體的自動化管理
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的多伺服器管理利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的自我微調功能。 因此，在正常情況下，不需要執行其他作業微調。 不過，當您執行作業時，網路負載會增加、產生警示並通知操作員。 您可以微調企業整體的自動化管理，將這些活動產生的網路流量降到最低。  
  
## <a name="see-also"></a>另請參閱  
[監視資料流程引擎的效能](../../integration-services/performance/performance-counters.md)  
  
