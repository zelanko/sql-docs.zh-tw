---
title: MSSQLSERVER_10539 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8334c28865c01c63ae6bcb18c79d4fd88b715175
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68060603"
---
# <a name="mssqlserver_10539"></a>MSSQLSERVER_10539
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10539|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_NO_PLAN_FOR_STMT|  
|訊息文字|無法從快取建立計畫指南 '%.*ls'，因為起始位移為 %d 的陳述式無法使用查詢計劃。 如果陳述式相依於尚未建立的資料庫物件，就可能發生這種問題。 請確定是否所有必要的資料庫物件都存在，並先建立計畫指南後再執行陳述式。|  
  
## <a name="explanation"></a>說明  
具有指定之起始位移的陳述式無法使用計畫快取中的查詢計劃。  
  
## <a name="user-action"></a>使用者動作  
請確定是否所有必要的資料庫物件都存在，並先建立計畫指南後再執行陳述式。  
  
## <a name="see-also"></a>另請參閱  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
