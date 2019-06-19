---
title: MSSQLSERVER_21889 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21889 (Database Engine error)
ms.assetid: ae199540-7986-4cc2-b782-cd22793236d3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 635205cbc92121034cd8c949382c4910c794b55e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63045821"
---
# <a name="mssqlserver21889"></a>MSSQLSERVER_21889
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|21889|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum21889|  
|訊息文字|SQL Server 執行個體 '%s' 並不是複寫發行者。 請在 SQL Server 執行個體 '%s' (具備散發者 '%s' ) 上執行 **sp_adddistributor**，以便讓執行個體裝載發行資料庫 '%s'。 請確定將其登入和密碼指定為與原始發行者所使用者相同。|  
  
## <a name="explanation"></a>說明  
若要裝載發行者資料庫， SQL Server 執行個體必須是複寫發行者。 **sp_validate_redirected_publisher**會呼叫遠端伺服器上的 **sp_helpdistributor**，以便判斷伺服器是否為複寫發行者。 此錯誤表示 SQL Server 的目標執行個體不是複寫發行者。  
  
## <a name="user-action"></a>使用者動作  
請在裝載發行者資料庫的 SQL Server 執行個體上執行 **sp_adddistributor**。 執行 **sp_adddistributor** 時，請指定正確的散發者。 針對 *@password* 參數，請使用與 **sp_adddistributor** 一開始在散發者端執行時使用的相同值。  
  
