---
description: 指定事件轉送伺服器
title: 指定事件轉送伺服器
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c6642a2cd8eac59cf20e8b0f9cb74482870f27ff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463091"
---
# <a name="designate-an-events-forwarding-server"></a>指定事件轉送伺服器
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 受控執行個體](https://docs.microsoft.com/azure/azure-sql/managed-instance/sql-managed-instance-paas-overview)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [SQL Server 中的 Azure SQL ManagSQL 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中指定 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將事件轉送到哪一部伺服器。 請注意，事件轉送適用於在伺服器之間轉送的事件，而不適用於在單一電腦上裝載之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間轉送的事件。 同時請注意，若要接收轉送的事件，則警示管理伺服器必須是預設的 SQL Server 執行個體。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
### <a name="security"></a><a name="Security"></a>安全性  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissions  
需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-designate-an-events-forwarding-server"></a>指定事件轉送伺服器  
  
1.  在 **[物件總管]** 中，按一下加號展開伺服器，從此伺服器轉送事件到另一部伺服器。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]，然後選取 [屬性]。  
  
3.  在 [SQL Server Agent 屬性 - <伺服器名稱>]****__ 對話方塊的 [選取頁面]**** 下，選取 [進階]****。  
  
4.  在 **[SQL Server 事件轉送]** 下，選取 **[轉送事件到另一部伺服器]** 核取方塊。  
  
5.  在 **[伺服器]** 清單中選取伺服器，然後在 **[事件]** 下選取下列其中一項：  
  
    -   選取 **[未處理的事件]** ，只轉送本機警示尚未處理的事件。  
  
    -   選取 **[所有事件]** ，轉送所有的事件，不論本機警示是否已處理。  
  
6.  在 **[如果事件的嚴重性等於或高於]** 清單中，按一下會開始將事件轉送至選定伺服器的嚴重性層級。  
  
7.  完成後，請按一下 **[確定]** 。  
  
