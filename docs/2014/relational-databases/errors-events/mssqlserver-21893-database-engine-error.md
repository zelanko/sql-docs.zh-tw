---
title: MSSQLSERVER_21893 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21893 (Database Engine error)
ms.assetid: 1ab1195a-fe2a-4e06-b871-b177b6bea1fe
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6258f36990efccf83b43e8d8ac8bd4c2397477aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914943"
---
# <a name="mssqlserver21893"></a>MSSQLSERVER_21893
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|21893|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum21893|  
|訊息文字|原始發行者 '%s' 的訂閱者 ( %s ) 並未在重新導向的發行者 '%s' 上顯示為遠端伺服器。 執行`sp_addlinkedserver`重新導向的發行者，將這些訂閱者新增為遠端伺服器。|  
  
## <a name="explanation"></a>說明  
 `sp_validate_redirected_publisher` 使用位於遠端伺服器的發行者資料庫的訂用帳戶中繼資料資料表，來識別其相關聯的訂閱者，並確認訂閱者的 master.dbo.sysservers 中有相關聯的項目。 如果任何識別的訂閱者不存在，就會傳回此錯誤。  
  
 此錯誤不會被視為嚴重錯誤。 發生此錯誤的代理程式會將錯誤記錄成參考用訊息但不會終止，因為新的發行者沒有適當的訂閱者項目對於複寫所造成的影響很有限。 如果 sysservers 中沒有適當的訂閱者項目，透過 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 執行的某些訂閱管理活動可能會失敗。 不過，只要明確執行管理預存程序，就可以成功執行這些相同的活動。  
  
## <a name="user-action"></a>使用者動作  
 請在每個識別訂閱者的重新導向發行者上執行 `sp_addlinkedserver`，以便將它們加入做為遠端伺服器。 然後，請執行 `sp_serveroption` 以設定伺服器的訂閱者位元。  
  
  
