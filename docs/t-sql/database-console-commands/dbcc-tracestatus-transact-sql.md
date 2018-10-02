---
title: DBCC TRACESTATUS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_TRACESTATUS_TSQL
- DBCC TRACESTATUS
- TRACESTATUS_TSQL
- TRACESTATUS
dev_langs:
- TSQL
helpviewer_keywords:
- global trace flags [SQL Server]
- status information [SQL Server], trace flags
- trace flags [SQL Server], status information
- DBCC TRACESTATUS statement
- session trace flags [SQL Server]
- displaying trace flag status
ms.assetid: 9be51199-78b4-4b87-ae6e-557246b7e29a
author: uc-msft
ms.author: umajay
manager: craigg
ms.openlocfilehash: 6a5f7d153bc518abde56995ea802f20f46531930
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47847543"
---
# <a name="dbcc-tracestatus-transact-sql"></a>DBCC TRACESTATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

顯示追蹤旗標的狀態。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DBCC TRACESTATUS ( [ [ trace# [ ,...n ] ] [ , ] [ -1 ] ] )   
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引數  
*trace#*  
這是會顯示狀態的追蹤旗標編號。 如果是 *trace#*，而且沒有指定 -1，則工作階段所啟用的所有追蹤旗標，都會全部顯示出來。
  
*n*  
這是一個預留位置，表示可以指定多個追蹤旗標。
  
-1  
顯示全域啟用的追蹤旗標狀態。 如果指定 -1，但沒有 *trace#*，則所有啟用的全域追蹤旗標都會顯示出來。
  
WITH NO_INFOMSGS  
抑制所有嚴重性層級在 0 到 10 的參考用訊息。
  
## <a name="result-sets"></a>結果集  
下表描述結果集中的資訊。
  
|資料行名稱|Description|  
|---|---|
|**TraceFlag**|追蹤旗標的名稱|  
|**狀態**|指出追蹤旗標是設為 ON 還是 OFF (無論是全域或工作階段)。<br /><br /> 1 = ON <br /><br /> 0 = OFF|  
|**全域**|指出追蹤旗標是否為全域設定<br /><br /> 1 = True<br /><br /> 0 = False|  
|**工作階段**|指出追蹤旗標是否針對工作階段而設定<br /><br /> 1 = True<br /><br /> 0 = False|  
  
DBCC TRACESTATUS 會傳回一個資料行代表追蹤旗標編號，以及一個資料行代表狀態。 其目的是指出追蹤旗標是 ON (1) 還是 OFF (0)。 追蹤旗標編號的資料行標題是**全域追蹤旗標**或**工作階段追蹤旗標**，這會隨著您所檢查的是全域追蹤旗標狀態還是工作階段追蹤旗標狀態而不同。
  
## <a name="remarks"></a>Remarks  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中有兩種類型的追蹤旗標：工作階段和全域。 工作階段追蹤旗標用於某個連接，而且只會在該連接顯示出來。 全域追蹤旗標是設在伺服器層級，只要是該伺服器上的連接，都看得到它們。
  
## <a name="permissions"></a>[權限]  
需要 **public** 角色的成員資格。
  
## <a name="examples"></a>範例  
下列範例會顯示目前全域啟用之所有追蹤旗標的狀態。
  
```sql  
DBCC TRACESTATUS(-1);  
GO  
```  
  
下列範例會顯示追蹤旗標 `2528` 和 `3205` 的狀態。
  
```sql  
DBCC TRACESTATUS (2528, 3205);  
GO  
```  
  
下列範例會顯示追蹤旗標 `3205` 是否全域啟用。
  
```sql  
DBCC TRACESTATUS (3205, -1);  
GO  
```  
  
下列範例會列出所有針對目前工作階段而啟用的追蹤旗標。
  
```sql  
DBCC TRACESTATUS();  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEOFF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACEON &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
[追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
