---
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 910fc06aac87eb846c0db76956eb45377fa3ecdb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034377"
---
# <a name="mssqlserver21871"></a>MSSQLSERVER_21871
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|21871|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum21871|  
|訊息文字|尚未重新導向資料庫 %s 的發行者 %s。|  
  
## <a name="explanation"></a>說明  
 `sp_validate_replica_hosts_as_publishers` 檢查資料表 MSredirected_publishers 項目識別的發行者和發行者資料庫的散發資料庫中。  找不到任何項目時，`sp_validate_replica_hosts_as_publishers` 就會傳回錯誤 21871。  
  
## <a name="user-action"></a>使用者動作  
 `sp_validate_replica_hosts_as_publishers` 只與重新導向的發行者有關。 如果發行者資料庫是可用性群組的成員，請使用 `sp_redirect_publisher` 預存程序，讓發行者和發行者資料庫與可用性群組的可用性群組接聽程式名稱產生關聯。  
  
  