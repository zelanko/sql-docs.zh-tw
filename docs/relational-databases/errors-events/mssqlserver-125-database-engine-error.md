---
title: MSSQLSERVER_125 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- "125"
helpviewer_keywords:
- 125 (Database Engine error)
ms.assetid: 0f58338d-2ea0-48b8-8a20-c438b0940433
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c311a94b0af4c36fbcdfc4abefdc175752d5addf
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver125"></a>MSSQLSERVER_125
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|125|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|案例運算式的巢狀層級只能到 %d。|  
  
## <a name="explanation"></a>說明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 CASE 運算式中只允許 10 層的巢狀層級。  
  
## <a name="user-action"></a>使用者動作  
將 CASE 陳述式的層級降到 10 層以下。  
  
## <a name="see-also"></a>另請參閱  
[CASE &#40;Transact-SQL&#41;](~/t-sql/language-elements/case-transact-sql.md)  
  

