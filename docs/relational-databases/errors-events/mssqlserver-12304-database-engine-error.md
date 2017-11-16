---
title: MSSQLSERVER_12304 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 12304 (Database Engine error)
ms.assetid: a2c252c2-e815-4ac8-a101-7af5b32e3233
caps.latest.revision: "4"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 7fc3019b148e9ac0ca278b69f55d2e2c67b33ac0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver12304"></a>MSSQLSERVER_12304
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|12304|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|HK_UNSUPPORTED_IDENTITY_TABLE_VAR|  
|訊息文字|在原生編譯預存程序的內容之外使用記憶體最佳化資料表類型時，不支援該類型與其任何資料行搭配使用 IDENTITY 屬性。|  
  
## <a name="user-action"></a>使用者動作  
請勿使用將識別屬性與其任何資料行搭配使用的記憶體最佳化資料表類型。  
  
## <a name="see-also"></a>另請參閱  
[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
