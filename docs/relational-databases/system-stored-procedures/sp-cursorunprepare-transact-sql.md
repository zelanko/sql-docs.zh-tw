---
title: "sp_cursorunprepare (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursorunprepare_TSQL
- sp_cursorunprepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorunprepare
ms.assetid: b46d4813-c4a9-4f9d-9979-2b5082ecf06a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 36f6633bdf09844359e7b7b5249869328efc70c0
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="spcursorunprepare-transact-sql"></a>sp_cursorunprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  捨棄 sp_cursorprepare 中開發的執行計畫預存程序。 sp_cursorunprepare 的叫用方式指定 ID = 6，在表格式資料流 (TDS) 封包中的。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cursorunprepare handle  
```  
  
## <a name="arguments"></a>引數  
 *控制代碼*  
 是*處理*備妥的陳述式時，sp_cursorprepare 會傳回的值。  
  
## <a name="see-also"></a>請參閱  
 [sp_cursorprepare &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
