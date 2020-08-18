---
description: MSSQLSERVER_8621
title: MSSQLSERVER_8621 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8621 (Database Engine error)
ms.assetid: 67f59865-becd-4999-8bb0-90aedd7effbf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5aa58480e63e15b418d3bc2f0ebe38330fe71be3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88331514"
---
# <a name="mssqlserver_8621"></a>MSSQLSERVER_8621
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|8621|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|OPTIMIZER_STACK_OVERFLOW_ERR|  
|訊息文字|查詢處理器在查詢最佳化期間已用完堆疊空間。 請簡化查詢。|  
  
## <a name="explanation"></a>說明  
展開的查詢大小是造成這項錯誤最有可能的原因。 展開的查詢會取代原始查詢中其參照的每個檢視、計算資料行、[!INCLUDE[tsql](../../includes/tsql-md.md)] 函數與一般資料表運算式的定義，以及串聯式動作，例如更新次要索引、檢視和觸發程序。  
  
最有可能的情況是查詢的某個維度很大；例如，檢視定義參考的資料表數目，或是純量運算式非常大。  
  
## <a name="user-action"></a>使用者動作  
依據最大的維度，將該查詢分割成多項查詢，藉以簡化查詢。 請先移除實際上不需要的任何查詢元素，然後嘗試新增暫存資料表，並將查詢分割成兩項查詢。  只將查詢的某個部分移到子查詢、函數或一般資料表運算式並不夠，因為 [!INCLUDE[tsql](../../includes/tsql-md.md)] 編譯器會重新合併這些元素。  
  
