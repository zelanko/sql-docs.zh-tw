---
title: 警示屬性 - 新增警示 (回應頁面)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.alert.response.f1
ms.assetid: 72daf008-f9ea-4077-b217-5048e7759d3e
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c8faf533bd04fb3052fa3678fd1da05cb36129de
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75254512"
---
# <a name="alert-properties---new-alert-response-page"></a>警示屬性 - 新增警示 (回應頁面)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此頁面可指定您想要執行的作業，並取得為回應 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示所要通知的操作員清單。  

## <a name="options"></a>選項。  
**執行作業**  
啟用 [作業清單]  、[新增作業]  和 [檢視作業]  選項。  
  
**新增作業**  
開啟 [新增作業]  對話方塊。 未選取 [執行作業]  時，無法使用這個按鈕。  
  
**檢視作業**  
檢視或修改選取的作業。 未選取 [執行作業]  時，無法使用這個選項。  
  
**通知操作員**  
可啟用讓您加入、移除或變更操作員的控制項。  
  
**操作員清單**  
列出發生警示時所要通知的操作員。 若要指定通知方法，請選取顯示於操作員名稱之後的 [電子郵件]  、[呼叫器]  或 [Net Send]  核取方塊。未選取 [通知操作員]  時，無法使用這個選項。  
  
**電子郵件**  
使用電子郵件通知操作員。  
  
**呼叫器**  
使用呼叫器電子郵件地址通知操作員。  
  
**Net Send**  
使用 **net send** 通知操作員。  
  
**新增操作員**  
顯示 [新增操作員]  對話方塊，可讓您建立新的操作員。  
  
**檢視操作員**  
顯示目前選取之操作員的 [屬性]  對話方塊。 您可以在 [操作員屬性]  對話方塊上檢視及修改操作員屬性。  
  
## <a name="see-also"></a>另請參閱  
[警示](../../ssms/agent/alerts.md)  
[Create an Alert Using Severity Level](../../ssms/agent/create-an-alert-using-severity-level.md)  
[警示](../../ssms/agent/alerts.md)  
[Edit an Alert](../../ssms/agent/edit-an-alert.md)  
[Delete an Alert](../../ssms/agent/delete-an-alert.md)  
  
