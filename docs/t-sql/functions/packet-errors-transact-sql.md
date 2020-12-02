---
description: '&#x40;&#x40;PACKET_ERRORS (Transact-SQL)'
title: '@@PACKET_ERRORS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@PACKET_ERRORS'
- '@@PACKET_ERRORS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@PACKET_ERRORS function'
- number of packet errors
- packets [SQL Server], errors
- networking [SQL Server], packet errors
- connections [SQL Server], packets
ms.assetid: f7da1b80-5cbe-42fa-be71-40c6af16383a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1470d95dd12134abf0e097e4c56f7eb908c807f0
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124613"
---
# <a name="x40x40packet_errors-transact-sql"></a>&#x40;&#x40;PACKET_ERRORS (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上次啟動之後，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接上所發生的網路封包錯誤數目。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
@@PACKET_ERRORS  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別
 **integer**  
  
## <a name="remarks"></a>備註  
 若要顯示包含多項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 統計資料的報表，其中包括封包錯誤數，請執行 **sp_monitor**。  
  
## <a name="examples"></a>範例  
 下列範例會顯示如何使用 `@@PACKET_ERRORS`。  
  
```sql  
SELECT @@PACKET_ERRORS AS 'Packet Errors';  
```  
  
 範例結果集如下：  
  
```  
Packet Errors  
-------------  
0  
```  
  
## <a name="see-also"></a>另請參閱  
 [@@PACK_RECEIVED &#40;Transact-SQL&#41;](../../t-sql/functions/pack-received-transact-sql.md)   
 [@@PACK_SENT &#40;Transact-SQL&#41;](../../t-sql/functions/pack-sent-transact-sql.md)   
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [系統統計函式 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
