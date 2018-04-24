---
title: MSSQLSERVER_21889 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 21889 (Database Engine error)
ms.assetid: ae199540-7986-4cc2-b782-cd22793236d3
caps.latest.revision: 6
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 425179a083707bb2504e9dc789c0a69aee3399d6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver21889"></a>MSSQLSERVER_21889
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|21889|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum21889|  
|訊息文字|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 '%s' 並不是複寫發行者。 請在具備散發者 '%s' 之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 '%s' 上執行 **sp_adddistributor**，以便讓執行個體主控發行資料庫 '%s'。 請確定將其登入和密碼指定為與原始發行者所使用者相同。|  
  
## <a name="explanation"></a>說明  
若要裝載發行者資料庫，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體必須是複寫發行者。 **sp_validate_redirected_publisher**會呼叫遠端伺服器上的 **sp_helpdistributor**，以便判斷伺服器是否為複寫發行者。 當 **sp_helpdistributor** 預存程序的執行結果指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目標執行個體不是複寫發行者時，就會傳回此錯誤。  
  
## <a name="user-action"></a>使用者動作  
請在裝載發行者資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上執行 **sp_adddistributor**。 執行 **sp_adddistributor** 時，請指定正確的散發者。 針對 *@password* 參數，請使用與 **sp_adddistributor** 一開始在散發者端執行時使用的相同值。  
  
