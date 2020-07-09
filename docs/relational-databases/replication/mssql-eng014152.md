---
title: MSSQL_ENG014152 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014152 error
ms.assetid: 4215e2b1-cd30-441f-9671-9afc742adf6e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 4225be7df1ceee87e3faf61e322975cb2a7a5694
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85721844"
---
# <a name="mssql_eng014152"></a>MSSQL_ENG014152
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
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
  
 使用 [sp_help_jobstep](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md) ，檢視要為指定複寫代理程式重試 **Run agent** 步驟的目前最大次數設定。 您可以使用 [sp_update_jobstep](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md) 預存程序的 `@retry_attempts` 參數來調整作業步驟重試次數。  
  
 如果重試訊息經常重複出現，請根據導致重試的訊息對此問題進行疑難排解。 請檢查代理程式的訊息記錄，找出必須排程進行重試的原因。 在某些情況下，您可能必須為複寫代理程式啟用更詳細的記錄。 如需有關如何設定複寫記錄的詳細資訊，請參閱 Microsoft 知識庫文件 [312292](https://support.microsoft.com/kb/312292)。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
