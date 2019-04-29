---
title: MSSQLSERVER_8966 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8966 (Database Engine error)
ms.assetid: 6b1150fd-9dfd-4df9-8f08-8eca237667db
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dee5b45aac6518517434595b0f26ce18d219866b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62913160"
---
# <a name="mssqlserver8966"></a>MSSQLSERVER_8966
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|8966|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC3_FAILED_TO_READ_AND_LATCH_PAGE|  
|訊息文字|無法使用閂鎖類型 TYPE 來讀取和閂鎖頁面 P_ID。 作業失敗。|  
  
## <a name="explanation"></a>說明  
頁面讀取失敗或無法針對 PFS 或 GAM 頁面採用閂鎖。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中可能有閂鎖逾時或其他隨附的訊息。  
  
## <a name="user-action"></a>使用者動作  
請檢閱 SQL 錯誤記錄檔，以便找出隨附的訊息並解決這些錯誤。  
  
