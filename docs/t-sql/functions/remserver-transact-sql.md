---
description: '&#x40;&#x40;REMSERVER (Transact-SQL)'
title: '@@REMSERVER (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@REMSERVER'
- '@@REMSERVER_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], remote servers
- remote servers [SQL Server], logins
- '@@REMSERVER function'
ms.assetid: 0bb451a9-3866-4064-963d-b74a2f864049
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 385f492a91e740dfea04f83b1da8c8a67861f05b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417204"
---
# <a name="x40x40remserver-transact-sql"></a>&#x40;&#x40;REMSERVER (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]請改用連結伺服器和連結伺服器預存程序。  
  
 傳回符合登入記錄所顯示的遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫伺服器的名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@REMSERVER  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別
 **nvarchar(128)**  
  
## <a name="remarks"></a>備註  
 @@REMSERVER 使預存程序能夠檢查執行這個程序的資料庫伺服器名稱。  
  
## <a name="examples"></a>範例  
 下列範例會建立傳回遠端伺服器名稱的 `usp_CheckServer` 程序。  
  
```  
CREATE PROCEDURE usp_CheckServer  
AS  
SELECT @@REMSERVER;  
```  
  
 下列預存程序建立在本機伺服器 `SEATTLE1` 上。 使用者會登入 `LONDON2` 遠端伺服器，並執行 `usp_CheckServer`。  
  
```  
EXEC SEATTLE1...usp_CheckServer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------  
LONDON2  
```  
  
## <a name="see-also"></a>另請參閱  
 [組態函式 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [遠端伺服器](../../database-engine/configure-windows/remote-servers.md)  
  
  
