---
description: 作業的挑選排程
title: 作業的挑選排程
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.pickscheduleforjob.f1
helpviewer_keywords:
- Pick Schedule for Job dialog box
ms.assetid: 6de2025d-c25c-47b9-9a25-18c294935c15
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 860d949cf17c41daee42a3261785e5b067b32ce0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474419"
---
# <a name="pick-schedule-for-job"></a>作業的挑選排程
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 受控執行個體](/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資訊，請參閱 [Azure SQL 受控執行個體與 SQL Server 之間的差異](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此對話方塊來挑選 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業的現有排程。  
  
## <a name="options"></a>選項  
**可用的排程**  
列出此作業可用的排程。 因為作業和排程必須有相同的擁有者，所以此清單只會包含工作擁有者所擁有的排程。  
  
**Name**  
顯示排程名稱。  
  
**Enabled**  
選取是否啟用排程。  
  
**說明**  
描述排程執行作業所用的條件。  
  
**排程中的作業**  
列出附加至排程的作業編號。 按一下某個編號以檢視該作業的屬性。  
  
**屬性**  
啟動 [作業排程屬性] 對話方塊，您可以在其中檢視排程的相關資訊。  
  
## <a name="see-also"></a>另請參閱  
[建立及附加排程至作業](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
