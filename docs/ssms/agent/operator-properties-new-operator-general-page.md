---
title: 新增操作員屬性 (一般頁面)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.operator.general.f1
ms.assetid: c036d1c9-83d1-4a95-b67e-29d283b1a046
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 73aa6081584ef3ae99206808631abc05e4674bae
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247664"
---
# <a name="operator-properties---new-operator-general-page"></a>操作員屬性 - 新增操作員 (一般頁面)

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此頁面來檢視和修改 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 操作員的一般屬性。  
  
## <a name="options"></a>選項。  
**名稱**  
變更操作員的名稱。  
  
**已啟用**  
啟用操作員。 未啟用時，不會傳送通知給操作員。  
  
**電子郵件名稱**  
指定操作員的電子郵件地址。  
  
**Net Send 位址**  
指定用於 **net send**的位址。  
  
**呼叫器電子郵件名稱**  
指定操作員呼叫器所用的電子郵件地址。  
  
**傳呼待命排程**  
設定呼叫器使用中的時間。  
  
**星期一至星期日**  
選取呼叫器使用中的日子。  
  
**工作日開始**  
選取時間，在該時間之後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 就會傳送訊息給呼叫器。  
  
**工作日結束**  
選取時間，在該時間之後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 就不再傳送訊息給呼叫器。  
  
## <a name="see-also"></a>另請參閱  
[運算子](../../ssms/agent/operators.md)  
  
