---
title: '@@TIMETICKS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@TIMETICKS_TSQL'
- '@@TIMETICKS'
dev_langs:
- TSQL
helpviewer_keywords:
- ticks [SQL Server]
- '@@TIMETICKS function'
- microseconds per tick [SQL Server]
- time [SQL Server], ticks
- number of microseconds per tick
ms.assetid: 9d036633-837f-4309-9c45-3d9600258018
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d8a1d9a1f3a4e12c790d42ab12de75f96ca1f7c1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818396"
---
# <a name="x40x40timeticks-transact-sql"></a>&#x40;&#x40;TIMETICKS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回每個刻度的百萬分之一秒數。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
@@TIMETICKS  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>Remarks  
 每個刻度的時間量，要視電腦而定。 作業系統上的每個刻度是 31.25 毫秒，或是三十分之一秒。  
  
## <a name="examples"></a>範例  
  
```  
SELECT @@TIMETICKS AS 'Time Ticks';  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統統計函式 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
