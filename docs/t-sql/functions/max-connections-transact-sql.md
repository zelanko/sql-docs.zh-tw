---
title: '@@MAX_CONNECTIONS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0066488fd917e5ffbe88767318954c1727adf238
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130332"
---
# <a name="x40x40maxconnections-transact-sql"></a>&#x40;&#x40;MAX_CONNECTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所能接受的最大同時使用者連接數目。 傳回的數目不一定是目前所設定的數目。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@MAX_CONNECTIONS  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>Remarks  
 允許的實際使用者連接數目也會隨著安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本及應用程式和硬體的限制而不同。  
  
 若要為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新設定較少的連線，請使用 **sp_configure**。  
  
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
 [組態函式](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [設定 user connections 伺服器組態選項](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
  
  
