---
title: MSSQL_ENG004929 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG004929 error
ms.assetid: 1d9b1d88-1fbf-4089-b392-687d3b0220ca
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f5e6b5d9957850a6e630695294059cc06024789b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134588"
---
# <a name="mssqleng004929"></a>MSSQL_ENG004929
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|4929|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|無法改變 %S_MSG '%.*ls'，因為它正在為複寫而發行。|  
  
## <a name="explanation"></a>說明  
 這個錯誤通常是在您嘗試在針對異動複寫所發行資料表上卸除主索引鍵條件約束時發生。 異動複寫的每個已發行資料表都需要主索引鍵，因此不能卸除條件約束。  
  
## <a name="user-action"></a>使用者動作  
 若要卸除條件約束，請先卸除與資料表關聯的發行項。 如需詳細資訊，請參閱[在現有發行集中加入和卸除發行項](publish/add-articles-to-and-drop-articles-from-existing-publications.md)。 如果在未複寫的資料庫中發生這個錯誤，請執行 [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)，以確保資料庫中的物件不會標示為已複寫。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
