---
title: "@@MAX_CONNECTIONS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@MAX_CONNECTIONS'
- '@@MAX_CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- simultaneous connections [SQL Server]
- maximum number of simultaneous user connections
- '@@MAX_CONNECTIONS function'
- connections [SQL Server], simultaneous
- number of simultaneous user connections
ms.assetid: 57eb9f4b-548f-4212-9684-a11d831c4732
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 29910f9bc06335c4df10acf7663bfef92edffce2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40maxconnections-transact-sql"></a>（& s) #x 40; & #x 40。MAX_CONNECTIONS (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所能接受的最大同時使用者連接數目。 傳回的數目不一定是目前所設定的數目。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@MAX_CONNECTIONS  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>備註  
 允許的實際使用者連接數目也會隨著安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本及應用程式和硬體的限制而不同。  
  
 若要重新設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]較少的連線，使用**sp_configure**。  
  
## <a name="examples"></a>範例  
 下列範例會顯示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上傳回的最大使用者連接數目。 這個範例假設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會為少數的使用者連接重新設定。  
  
```  
SELECT @@MAX_CONNECTIONS AS 'Max Connections';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Max Connections  
---------------  
32767            
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [組態函數](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [設定 user connections 伺服器組態選項](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
  
  

