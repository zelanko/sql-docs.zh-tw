---
title: 微調企業整體的自動化管理 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- performance [SQL Server], automated administration
- tuning automated administration [SQL Server]
- monitoring performance [SQL Server], automated administration
ms.assetid: 671fed35-3859-4b0d-8f38-4dd07436857e
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 24ae20b48409b95dadf758722e6694d55cf9945f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="tune-automated-administration-across-an-enterprise"></a>微調企業整體的自動化管理
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 的多伺服器管理利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的自我微調功能。 因此，在正常情況下，不需要執行其他作業微調。 不過，當您執行作業時，網路負載會增加、產生警示並通知操作員。 您可以微調企業整體的自動化管理，將這些活動產生的網路流量降到最低。  
  
## <a name="see-also"></a>另請參閱  
[監視資料流程引擎的效能](http://msdn.microsoft.com/en-us/11e17f4e-72ed-44d7-a71d-a68937a78e4c)  
  
