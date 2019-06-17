---
title: SUSER_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUSER_NAME
- SUSER_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- identification names for logins [SQL Server]
- users [SQL Server], logins
- SUSER_NAME function
- logins [SQL Server], names
- names [SQL Server], logins
ms.assetid: ae598d9f-9baa-49b8-b1c1-042854206de4
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 507e198a12ad613602ffe77295313851f72ecb60
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65948000"
---
# <a name="susername-transact-sql"></a>SUSER_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

傳回使用者的登入識別名稱。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SUSER_NAME ( [ server_user_id ] )   
```  
  
## <a name="arguments"></a>引數  
_server\_user\_id_  
這是使用者的登入識別碼。 _server\_user\_id_ (選擇性) 為 **int**. _server\_user\_id_ 可以是有權連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者或群組。 未指定 _server\_user\_id_ 時，就會傳回目前使用者的登入識別名稱。 如果參數包含 NULL 一詞，就會傳回 NULL。  
  
## <a name="return-types"></a>傳回類型  
**nvarchar(128)**  
  
## <a name="remarks"></a>Remarks  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 版中，安全性識別碼 (SID) 取代了伺服器使用者識別碼 (SUID)。  
  
SUSER_NAME 只會傳回在 **syslogins** 系統資料表中有項目之登入的登入名稱。  
  
SUSER_NAME 可用於選取清單、WHERE 子句及任何允許使用運算式的位置。 請在 SUSER_NAME 之後使用括弧，即使未指定任何參數也一樣。  
  
## <a name="examples"></a>範例  
下列範例會傳回登入識別碼是 `1` 之使用者的登入識別名稱。  
  
```  
SELECT SUSER_NAME(1);  
```  
  
## <a name="see-also"></a>另請參閱  
[SUSER_ID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-id-transact-sql.md)   
[主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
