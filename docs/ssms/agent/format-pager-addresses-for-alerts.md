---
description: 設定警示的呼叫器位址格式
title: 設定警示的呼叫器位址格式
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- pager addresses [SQL Server]
- SQL Server Agent, alerts
- formats [SQL Server], pager addresses
- pager notifications [SQL Server]
- addresses [SQL Server]
- alerts [SQL Server], pager addresses
ms.assetid: a9797d01-1050-442c-9038-ed4bfee1e76a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: d5df0229f84063f11f80fdefa78afffc6b8e2d40
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97422887"
---
# <a name="format-pager-addresses-for-alerts"></a>設定警示的呼叫器位址格式
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 受控執行個體](/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL 受控執行個體與 SQL Server 之間的 T-SQL 差異](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中格式化 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示的呼叫器號碼。  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
### <a name="security"></a><a name="Security"></a>安全性  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissions  
依預設， **系統管理員 (sysadmin)** 固定伺服器角色的成員可以檢視警示的相關資訊。 其他使用者必須被授與 **msdb** 資料庫的 **SQLAgentOperatorRole** 固定資料庫角色。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-format-pager-addresses"></a>若要格式化呼叫器號碼  
  
1.  在 **[物件總管]** 中，按一下加號展開伺服器，此伺服器包含要傳送至呼叫器的警示。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]，然後選取 [屬性]。  
  
3.  在 **[選取頁面]** 底下，選取 **[警示系統]**。  
  
4.  在 [呼叫器電子郵件位址格式] 欄位的 [收件者] 和 [副本] 方塊中，輸入呼叫器號碼的前置詞和後置詞。 當傳送通知時，就會插入操作員的實際呼叫器號碼。  
  
5.  在 **[主旨]** 方塊中，輸入主旨行前置詞或後置詞。  
  
6.  選取 [將電子郵件的內文包含在通知訊息中] 核取方塊，表示會在呼叫器訊息中加入完整的電子郵件訊息 (而不是僅有主旨行)。  
  
7.  完成後，請按一下 **[確定]** 。  
