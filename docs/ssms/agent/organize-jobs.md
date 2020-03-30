---
title: 組織作業
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job category
- organize jobs
ms.assetid: 629c3e06-f933-483b-8621-280dbb7a7bd1
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a02f50ed88a2883d0149dbbd37df63b27e87dfa4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75247607"
---
# <a name="organize-jobs"></a>組織作業
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

作業類別目錄可幫助您組織作業，以便於篩選與分組。 例如，您可以將所有的資料庫備份作業整理在資料庫維護類別中。 您也可以建立您自己的作業類別。  
  
> [!WARNING]  
> 多伺服器類別只存在於主要伺服器上。 主要伺服器上只有一個預設作業類別目錄：**未分類 (多伺服器)** 。 下載多伺服器作業之後，其類別目錄會變更為目標伺服器上的 **[來自 MSX 的作業]** 。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**說明**|**主題**|  
|描述如何建立作業類別目錄。|[建立作業類別目錄](../../ssms/agent/create-a-job-category.md)|  
|描述如何刪除作業類別目錄。|[刪除作業類別目錄](../../ssms/agent/delete-a-job-category.md)|  
|描述如何將作業指派給作業類別目錄。|[將作業指派至作業類別目錄](../../ssms/agent/assign-a-job-to-a-job-category.md)|  
|描述如何變更作業類別目錄的成員資格。|[Change the Membership of a Job Category](../../ssms/agent/change-the-membership-of-a-job-category.md)|  
|描述如何列出類別目錄資訊。|[列出作業類別目錄資訊](../../ssms/agent/list-job-category-information.md)|  
  
