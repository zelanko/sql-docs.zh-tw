---
title: MSSQLSERVER_21899 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 21899 (Database Engine error)
ms.assetid: 32b87a7c-5380-4638-b147-dd78618f6625
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 957cb58c292f895e31ae01d9918af4872a29bd9d
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415407"
---
# <a name="mssqlserver21899"></a>MSSQLSERVER_21899
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|21899|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum21899|  
|訊息文字|在重新導向發行者 '%s' 上進行的查詢，可判斷原始發行者 '%s' 的訂閱者是否有 sysserver 項目失敗，發生錯誤 '%d'，錯誤訊息 '%s'。|  
  
## <a name="explanation"></a>說明  
 `sp_validate_redirected_publisher` 會查詢位於遠端伺服器之發行者資料庫的訂閱中繼資料資料表，以便判斷其相關聯的訂閱者。 如果此查詢失敗，就會傳回錯誤 21899。 驗證查詢需要存取位於重新導向發行者的已發行資料庫。 如果針對原始發行者呼叫 `sp_adddistpublisher` 時指定的登入未經授權，無法存取位於重新導向發行者的已發行資料庫，就會傳回錯誤 21899。  
  
## <a name="user-action"></a>使用者動作  
 請檢閱引用的錯誤訊息，以便判斷失敗的原因並且採取適當的更正動作。  
  
  
