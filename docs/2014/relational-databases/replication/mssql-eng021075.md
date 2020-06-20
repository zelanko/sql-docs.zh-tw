---
title: MSSQL_ENG021075 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021075 error
ms.assetid: c8c29543-d1f6-49d5-b6c8-e8c3aa373090
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8895c225ca833dee7d9b8e1a08bce722dc40f8c8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010085"
---
# <a name="mssql_eng021075"></a>MSSQL_ENG021075
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|21075|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|發行集 '%s' 的初始快照集尚無法使用。|  
  
## <a name="explanation"></a>說明  
 如果在「快照集代理程式」完成快照集的產生之前啟動「散發代理程式」或「合併代理程式」，會引發錯誤 MSSQL_ENG021075。  
  
## <a name="user-action"></a>使用者動作  
 如果在建立訂閱或上次選擇重新初始化訂閱後未啟動發行集的「快照集代理程式」，請啟動「快照集代理程式」，並讓其在啟動「散發代理程式」或「合併代理程式」之前完成。 如需詳細資訊，請參閱[建立和套用快照集](create-and-apply-the-snapshot.md)。  
  
 若快照集代理程式未完成，請檢查快照集代理程式記錄，以便找出錯誤並加以解決。 如需有關在「複寫監視器」中檢視代理程式狀態和錯誤詳細資料的資訊，請參閱[使用複寫監視器來檢視資訊及執行工作](monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
 若錯誤繼續發生，請增加代理程式的記錄，並指定記錄的輸出檔。 視錯誤內容的不同，可提供導致錯誤的步驟和 (或) 其他錯誤訊息。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
