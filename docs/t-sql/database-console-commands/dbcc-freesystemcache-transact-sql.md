---
title: DBCC FREESYSTEMCACHE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FREESYSTEMCACHE_TSQL
- DBCC_FREESYSTEMCACHE_TSQL
- DBCC FREESYSTEMCACHE
- FREESYSTEMCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- clearing unused cache entries
- DBCC FREESYSTEMCACHE statement
- unused cache entries
- releasing unused cache entries
- freeing unused cache entries
- cleaning unused cache entries
ms.assetid: 4b5c460b-e4ad-404a-b4ca-d65aba38ebbb
author: pmasl
ms.author: umajay
ms.openlocfilehash: 31b5731dc0507ebab3dd27fb6e12d3a501428898
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85685532"
---
# <a name="dbcc-freesystemcache-transact-sql"></a>DBCC FREESYSTEMCACHE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

釋出所有快取中所有未使用的快取項目。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會主動在背景清除未使用的快取項目，讓記憶體存放目前的項目。 不過，您可以使用這個命令，以手動方式從每個快取或是所指定 Resource Governor 集區快取中移除未使用的項目。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
```syntaxsql
DBCC FREESYSTEMCACHE   
    ( 'ALL' [, pool_name ] )   
    [WITH   
    { [ MARK_IN_USE_FOR_REMOVAL ] , [ NO_INFOMSGS ]  }  
    ]  
```  
  
## <a name="arguments"></a>引數  
( 'ALL' [,_pool\_name_ ] )  
ALL 會指定所有支援的快取。  
_pool\_name_ 會指定 Resource Governor 集區快取。 僅會釋放與此集區相關的項目。  
  
MARK_IN_USE_FOR_REMOVAL  
不再使用目前所用的項目之後，分別從其對應的快取中，以非同步的方式釋出這些項目。 在 DBCC FREESYSTEMCACHE WITH MARK_IN_USE_FOR_REMOVAL 執行之後，於快取中建立的新項目皆不受影響。  
  
NO_INFOMSGS  
隱藏所有參考訊息。  
  
## <a name="remarks"></a>備註  
執行 DBCC FREESYSTEMCACHE 會清除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的計劃快取。 清除計畫快取會導致重新編譯所有未來執行計畫，且可能會導致查詢效能突然暫時降低。 對於計劃快取中，各個已清除的快取存放區，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄會包含下列資訊訊息：「由於 'DBCC FREEPROCCACHE' 或 'DBCC FREESYSTEMCACHE' 作業，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 '%s' 快取存放區 (計劃快取的一部分) 發生 %d 次快取存放區排清。」 只要在該時間間隔內快取發生排清，這個訊息就會每五分鐘記錄一次。

## <a name="result-sets"></a>結果集  
DBCC FREESYSTEMCACHE 會傳回：「DBCC 的執行已經完成。 如果 DBCC 印出錯誤訊息，請連絡您的系統管理員」。
  
## <a name="permissions"></a>權限  
需要伺服器的 ALTER SERVER STATE 權限。
  
## <a name="examples"></a>範例  
  
### <a name="a-releasing-unused-cache-entries-from-a-resource-governor-pool-cache"></a>A. 從資源管理員集區快取釋放未使用的快取項目  
下列範例將說明如何清除指定之資源管理員資源集區所專用的快取。
  
```sql
-- Clean all the caches with entries specific to the resource pool named "default".  
DBCC FREESYSTEMCACHE ('ALL', default);  
```  
  
### <a name="b-releasing-entries-from-their-respective-caches-after-they-become-unused"></a>B. 等項目不用之後，分別從其對應的快取中釋出這些項目  
下列範例會使用 MARK_IN_USE_FOR_REMOVAL 子句，當項目不再使用之後，就從目前所有的快取中釋放這些項目。
  
```sql
DBCC FREESYSTEMCACHE ('ALL') WITH MARK_IN_USE_FOR_REMOVAL;  
```  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)  
[DBCC FREESESSIONCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)  
[資源管理員](../../relational-databases/resource-governor/resource-governor.md)
  
  
