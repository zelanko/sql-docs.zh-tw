---
title: sp_execute （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_execute
- sp_cursor_execute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute
ms.assetid: 2009acd3-0d92-435a-a8fb-057e50dc7146
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 12bfa6e7d37aae2a5ffc58828d47ace11d558487
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87392833"
---
# <a name="sp_execute-transact-sql"></a>sp_execute (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)]使用指定的控制碼和選擇性參數值，執行備妥的語句。 sp_execute 的叫用方式是在表格式資料流程（TDS）封包中指定 ID = 12。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_execute handle OUTPUT  
    [,bound_param  ]  [,...n ]  ]  
```  
  
## <a name="arguments"></a>引數  
 *圖*  
 這是 sp_prepare 所傳回的*控制碼*值。 *handle*是針對**int**輸入值呼叫的必要參數。  
  
 *bound_param*  
 表示使用其他參數。 *bound_param*是必要的參數，它會呼叫任何資料類型的輸入值，以表示程式的其他參數。  
  
> [!NOTE]  
>  *bound_param*必須符合 sp_prepare*params*值所做的宣告，其格式可以是* @name = 值*或*值*。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_prepare &#40;交易 SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)  
  
  
