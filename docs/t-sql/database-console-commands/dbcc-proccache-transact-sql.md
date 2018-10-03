---
title: DBCC PROCCACHE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC PROCCACHE
- DBCC_PROCCACHE_TSQL
- PROCCACHE_TSQL
- PROCCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- procedure cache [SQL Server]
- displaying procedure cache information
- DBCC PROCCACHE statement
ms.assetid: 7a4f9f8a-13ff-4bf2-ba29-c17012a23659
author: uc-msft
ms.author: umajay
manager: craigg
ms.openlocfilehash: 2d4580bb57680392c1e3901c2fd64b399c125736
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741106"
---
# <a name="dbcc-proccache-transact-sql"></a>DBCC PROCCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

以表格形式顯示程序快取區的相關資訊。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DBCC PROCCACHE [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引數  
 取代所有提及的  
 接受即將指定的選項。  
  
 NO_INFOMSGS  
 抑制所有嚴重性層級在 0 至 10 的參考訊息。  
  
## <a name="remarks"></a>Remarks  
程序快取用來快取已編譯和可執行的計畫，以加速批次的執行。 程序快取中的項目，屬於批次層級。 程序快取含有下列項目：
-   已編譯的計畫  
-   執行計畫  
-   Algebrizer 樹  
-   擴充程序  
  
## <a name="result-sets"></a>結果集  
下表將描述結果集的資料行。
  
|資料行名稱|Description|  
|-----------------|-----------------|  
|**num proc buffs**|程序快取中所有項目所用的總頁數。|  
|**num proc buffs used**|所有目前使用中的項目所用的總頁數。|  
|**num proc buffs active**|只是為了與舊版相容。 所有目前使用中的項目所用的總頁數。|  
|**proc cache size**|程序快取中的總項目數。|  
|**proc cache used**|目前使用中的總項目數。|  
|**proc cache active**|只是為了與舊版相容。 目前使用中的總項目數。|  
  
## <a name="permissions"></a>[權限]  
需要 **系統管理員** 固定伺服器角色或 **db_owner** 固定資料庫角色中的成員資格。
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
