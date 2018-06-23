---
title: MSSQL_ENG021331 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG021331 error
ms.assetid: 9acd75d9-fda1-44cd-ba17-20295ad53ea0
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3b0cbb943935514c6c9a6fc4589e3430146217cb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031616"
---
# <a name="mssqleng021331"></a>MSSQL_ENG021331
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|21331|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|無法將使用者指令碼檔案複製到散發者。(%ls)|  
  
## <a name="explanation"></a>說明  
 當手動初始化訂閱，且由複寫產生或在複寫命令中指定的指令碼無法儲存至指定目錄時，可能會出現此錯誤。 錯誤可能是權限問題所造成：當訂閱沒有使用快照集初始化，在發行者端執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶，就必須要有散發者端之快照集資料夾的寫入權限。  
  
## <a name="user-action"></a>使用者動作  
 請確定指定的快照集資料夾路徑正確，而且在發行者端執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶具有足夠的權限。  
  
## <a name="see-also"></a>另請參閱  
 [指定預設快照集位置 &#40;SQL Server Management Studio&#41;](specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)   
 [不使用快照集初始化交易式訂閱](initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  