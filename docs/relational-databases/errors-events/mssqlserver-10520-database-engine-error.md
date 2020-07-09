---
title: MSSQLSERVER_10520 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8f83b574d6201d0845f23c9194ea2e873d90daa5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781486"
---
# <a name="mssqlserver_10520"></a>MSSQLSERVER_10520
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|10520|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PG_PARAM_NOT_ALLOWED|  
|訊息文字|無法建立計畫指南 '%.*ls'，因為已將 @type 指定為 '%ls'，而且已為參數 '%ls' 指定非 NULL 值， 但這種類型要求參數必須為 NULL 值。 請為參數指定 NULL，或將參數類型變更為允許非 NULL 值的類型。|  
  
## <a name="explanation"></a>說明  
在 @type 中指定的類型要求指定的參數必須為 NULL 值，但是卻提供了非 NULL 值。  
  
## <a name="user-action"></a>使用者動作  
請為參數指定 NULL，或將參數類型變更為允許非 NULL 值的類型。  
  
## <a name="see-also"></a>另請參閱  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[計畫指南](~/relational-databases/performance/plan-guides.md)  
  
