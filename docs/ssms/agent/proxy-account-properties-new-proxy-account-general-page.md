---
title: Proxy 帳戶屬性 - 新 Proxy 帳戶 (一般頁面) | Microsoft Docs
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
f1_keywords:
- sql13.ag.proxy.general.f1
ms.assetid: 5cd81265-bf59-413b-8397-150ddc70d0c7
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b58f5c87bf872654a5c4bda78433d54785194831
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="proxy-account-properties---new-proxy-account-general-page"></a>Proxy 帳戶屬性 - 新增 Proxy 帳戶 (一般頁面)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此頁面檢視或變更 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 的 Proxy 帳戶屬性。  
  
## <a name="options"></a>選項。  
**Proxy 名稱**  
鍵入 Proxy 的名稱。  
  
**認證名稱**  
鍵入 Proxy 的認證名稱。  
  
> [!NOTE]  
> 提供的認證名稱必須是現有的認證名稱。 如需如何建立認證的詳細資訊，請參閱 [如何︰建立 Proxy (SQL Server Management Studio)](http://msdn.microsoft.com/en-us/c1e77e91-2a69-40d9-b8b3-97cffc710586)  
  
**...**  
啟動 [選取認證] 對話方塊。  
  
**說明**  
輸入 Proxy 的描述。  
  
**對下列子系統有效**  
選取 Proxy 帳戶可以存取的子系統。  
  
**重新指派作業步驟給**  
選取要被重新指派作業步驟的 Proxy。 當撤銷存取 Proxy 先前已存取過的子系統時，會啟用此清單。  
  
## <a name="see-also"></a>另請參閱  
[建立 SQL Server Agent Proxy](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
  
