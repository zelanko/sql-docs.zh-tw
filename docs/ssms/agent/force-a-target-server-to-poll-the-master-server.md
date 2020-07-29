---
title: 強制目標伺服器輪詢主要伺服器
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- forcing master server polling
- polling master servers [SQL Server]
- master servers [SQL Server], polling
- target servers [SQL Server], polling the master server
ms.assetid: f1189a47-5ac3-45e2-9c5f-847810672279
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5e0dc40d29ed0efd8dd6ce95172c63a1e1a853b0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715806"
---
# <a name="force-a-target-server-to-poll-the-master-server"></a>強制目標伺服器輪詢主要伺服器
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何強制目標伺服器輪詢主要伺服器。 目標伺服器必須是主要伺服器上已註冊的伺服器。  
  
作業是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 執行的一系列指定動作。 多重伺服器作業是一個主要伺服器執行於一或多個目標伺服器上的作業。 每一個目標伺服器可以同時執行相同作業的一個執行個體。 每個目標伺服器會定期輪詢主要伺服器、下載任何指派到目標伺服器的新作業之副本，然後中斷連接。 目標伺服器會先在本機執行作業，然後再重新連接到主要伺服器，以便上傳作業結果的狀態。  
  
> [!NOTE]  
> 如果當目標伺服器嘗試上傳作業狀態時無法存取主要伺服器，作業狀態會被多工緩衝處理，直到可以存取主要伺服器為止。  
  
-   **開始之前：** [限制事項](#Restrictions)、[安全性](#Security)  
  
-   **若要強制目標伺服器輪詢主要伺服器，請使用：** [SQL Server Management Studio](#SSMS)  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>限制事項  
目標伺服器必須是主要伺服器上已註冊的伺服器。 您必須從主要伺服器執行本主題中提供的指示。  
  
### <a name="security"></a><a name="Security"></a>安全性  
如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md) ＞和＜ [Choose the Right SQL Server Agent Service Account for Multiserver Environments](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)＞。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>使用 SQL Server Management Studio  
**若要強制目標伺服器輪詢主要伺服器**  
  
1.  在 **[物件總管]** 中展開主要伺服器。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]  ，指向 [多重伺服器管理]  ，然後按一下 [管理目標伺服器]  。  
  
3.  按一下目標伺服器，然後按一下 **[強制輪詢]** 。  
  
