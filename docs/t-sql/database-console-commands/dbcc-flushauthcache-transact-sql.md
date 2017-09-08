---
title: "DBCC FLUSHAUTHCACHE (TRANSACT-SQL) |Microsoft 文件"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC FLUSHAUTHCACHE
- FLUSHAUTHCACHE
- DBCC_FLUSHAUTHCACHE_TSQL
- FLUSHAUTHCACHE_TSQL
helpviewer_keywords:
- DBCC FLUSHAUTHCACHE
ms.assetid: 681ef31d-ceb9-4da5-86bf-bf1240df950f
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3ba6a519ebcdbbc70bf19ec491539a3b07fb6c85
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-flushauthcache-transact-sql"></a>DBCC FLUSHAUTHCACHE (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

包含登入與目前使用者資料庫中的防火牆規則的相關資訊的資料庫驗證快取會清空[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。 本聲明不適用於的邏輯 master 資料庫，因為 master 資料庫中包含登入和防火牆規則的相關資訊的實體儲存體。 執行陳述式的使用者和其他目前連接的使用者保持連接。 (如目前不支援 DBCC FLUSHAUTHCACHE [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]。)
 
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DBCC FLUSHAUTHCACHE [ ; ]  
```  
  
## <a name="arguments"></a>引數  
無。
  
## <a name="remarks"></a>備註  
驗證快取建立登入與伺服器防火牆規則，會儲存在 master 中，並將它們放置在使用者資料庫中的記憶體中的複本。  因為自主的資料庫使用者的資訊已儲存在使用者資料庫中，自主的資料庫使用者不是驗證快取的一部分。
持續作用中的連線至[!INCLUDE[ssSDS](../../includes/sssds-md.md)]需要重新授權 (由執行[!INCLUDE[ssDE](../../includes/ssde-md.md)]) 至少每隔 10 小時。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]嘗試重新授權使用最初提交的密碼和使用者不需要輸入。 基於效能考量，當密碼重設[!INCLUDE[ssSDS](../../includes/sssds-md.md)]，此連接將不會重新驗證，即使因為連接共用會重設連接。 這是在內部部署的行為不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果密碼已變更，因為一開始授權連接，連接必須終止，並使用新的密碼時，建立新的連接。 KILL DATABASE CONNECTION 權限的使用者可以明確地結束連接[!INCLUDE[ssSDS](../../includes/sssds-md.md)]使用[KILL & #40;TRANSACT-SQL & #41;](../../t-sql/language-elements/kill-transact-sql.md)命令。
  
## <a name="permissions"></a>Permissions  
需要[!INCLUDE[ssSDS](../../includes/sssds-md.md)]系統管理員帳戶。
  
## <a name="example"></a>範例  
下列陳述式會清除驗證快取目前的資料庫。
  
```sql
DBCC FLUSHAUTHCACHE;  
```  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  

