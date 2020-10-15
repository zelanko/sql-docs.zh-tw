---
description: 調整作業記錄大小
title: 調整作業記錄大小
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- resizing job history log
- size [SQL Server], job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: ddee1ce8-9d1b-4017-9894-bf7256aed95d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 122f94d8eab17caf22d532c1dd81fec31c334205
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037831"
---
# <a name="resize-the-job-history-log"></a>調整作業記錄大小

[!INCLUDE[applies-to-version/_ssnoversion.md](../../includes/applies-to-version/sqlserver.md)]

> [!IMPORTANT]  
> [Azure SQL 受控執行個體](/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL 受控執行個體與 SQL Server 之間的 T-SQL 差異](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主題描述如何使用 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 來設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Agent 作業記錄的大小限制。

- **開始之前：**  

    [安全性](#Security)  

- **若要使用下列項目設定作業記錄的大小限制：**  

    [Transact-SQL](#SSMS)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  

### <a name="security"></a><a name="Security"></a>安全性

如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)＞。  

## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>使用 SQL Server Management Studio

根據原始大小重新調整作業記錄與記錄

1. 在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。

2. 以滑鼠右鍵一下 [SQL Server Agent]，然後選取 [屬性]。

3. 選取 [記錄]  頁面，然後確認已選取 [限制作業記錄大小]  。

4. 在 **[最大作業記錄大小]** 方塊中，輸入作業記錄所允許的最大資料列數。

5. 在 **[每項作業的作業記錄最大資料列數]** 方塊中，輸入作業所允許的最大作業記錄資料列數。

**根據時間重新調整作業記錄和記錄：**

1. 在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  

2. 以滑鼠右鍵一下 [SQL Server Agent]，然後選取 [屬性]。

3. 選取 [記錄] 頁面，然後選取 [移除代理程式記錄]。

4. 選取適當的 [天]  、[週]  或 [月]  數。