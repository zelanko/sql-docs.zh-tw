---
title: "使用中央管理伺服器管理多部伺服器 | Microsoft Docs"
ms.custom: 
ms.date: 08/12/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: relational-databases-misc
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiserver queries
- central management server
- multiserver administration [SQL Server]
- master servers [SQL Server], central management servers
- target configuration [SQL Server]
- server configuration [SQL Server]
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a746ab7863c97e7738760f863227c7d1c0020644
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2018
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>使用中央管理伺服器管理多部伺服器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
您可以透過指定中央管理伺服器並建立伺服器群組來管理多部伺服器。  
  
## <a name="what-is-a-central-management-server-and-server-groups"></a>什麼是中央管理伺服器和伺服器群組？  
 指定為中央管理伺服器的 SQL Server 執行個體，會針對一個或多個執行個體維護含有連接資訊的伺服器群組。 您可以針對伺服器群組同時執行 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式和原則式管理原則。 您也可以在透過中央管理伺服器所管理的執行個體上檢視記錄檔。 
 
 基本上，中央管理伺服器是包含您受管理伺服器清單的中央存放庫。 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 之前的版本無法指定為中央管理伺服器。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式。  
  
## <a name="create-central-management-server-and-server-groups"></a>建立中央管理伺服器和伺服器群組 
 若要建立中央管理伺服器和伺服器群組，請使用 **中的** [已註冊的伺服器] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]視窗。 請注意，中央管理伺服器不可以是它所維護之群組的成員。 
 
 如需如何建立中央管理伺服器和伺服器群組的詳細資訊，請參閱[建立中央管理伺服器和伺服器群組 &#40;SQL Server Management Studio&#41;](../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來管理伺服器](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
