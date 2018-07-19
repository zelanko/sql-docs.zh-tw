---
title: MSSQL_ENG014152 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014152 error
ms.assetid: 4215e2b1-cd30-441f-9671-9afc742adf6e
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4b499d24a6cfa7c09f75d0d0150eb8f2f942d4b7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37205218"
---
# <a name="mssqleng014152"></a>MSSQL_ENG014152
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|14152|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|複寫 -%s：代理程式 %s 已排程重試。 %s|  
  
## <a name="explanation"></a>說明  
 指定的複寫代理程式已經排程重試要求的作業。 處理序會繼續重試，直到到達為作業步驟所設定的最大重試嘗試次數。  
  
 重試通常是因為下列其中一個原因而發生：  
  
-   已超出 **QueryTimeout** 值。  
  
-   已超出 **LoginTimeout** 值。  
  
-   複寫處理序已被選擇做為死結的犧牲者。  
  
## <a name="user-action"></a>使用者動作  
 如果重試訊息不頻繁，則不需要任何使用者動作。  
  
 使用 [sp_help_jobstep](/sql/relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql) ，檢視要為指定複寫代理程式重試 **Run agent** 步驟的目前最大次數設定。 您可以使用 **@retry_attempts** 預存程序的 [@retry_attempts](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql) 參數，調整作業步驟重試的次數。  
  
 如果重試訊息經常重複出現，請根據導致重試的訊息對此問題進行疑難排解。 請檢查代理程式的訊息記錄，找出必須排程進行重試的原因。 在某些情況下，您可能必須為複寫代理程式啟用更詳細的記錄。 如需有關如何設定複寫記錄的詳細資訊，請參閱 Microsoft 知識庫文件 [312292](http://support.microsoft.com/kb/312292)。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
