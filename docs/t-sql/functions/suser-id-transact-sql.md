---
title: "SUSER_ID (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_ID_TSQL
- SUSER_ID
dev_langs:
- TSQL
helpviewer_keywords:
- users [SQL Server], IDs
- logins [SQL Server], IDs
- SUSER_ID function
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- user IDs [SQL Server]
ms.assetid: 348911ab-b0b6-4867-aee7-e6f42e053a4a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e4b00485c741857f1e3438c3e50995886900fe29
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="suserid-transact-sql"></a>SUSER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回使用者的登入識別碼。  
  
> [!NOTE]  
>  從開始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，SUSER_ID 會傳回做為所列的值**principal_id**中**sys.server_principals**目錄檢視。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SUSER_ID ( [ 'login' ] )   
```  
  
## <a name="arguments"></a>引數  
 **'** *登入* **'**  
 這是使用者的登入名稱。 *登入*是**nchar**。 如果*登入*指定為**char**，*登入*隱含地轉換成**nchar**。 *登入*可以是任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入或 Windows 使用者或群組是否有權限連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果*登入*是未指定，會傳回目前使用者的登入識別碼。 如果參數包含 NULL 一詞，就會傳回 NULL。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="remarks"></a>備註  
 SUSER_ID 只會針對在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內明確規定的登入來傳回識別碼。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內，這個識別碼是用來追蹤擁有權和權限。 這個識別碼不等於 SUSER_SID 傳回之登入的 SID。 如果*登入*是 SQL Server 登入，則 SID 會對應至 GUID。 如果*登入*是 Windows 登入或 Windows 群組，則 SID 會對應至 Windows 安全性識別碼。  
  
 SUSER_SID 傳回僅針對具有項目中的登入的 SUID **syslogins**系統資料表。  
  
 系統函數可用在選取清單、WHERE 子句及任何允許使用運算式的位置中，且後面一律必須接著括號，即使未指定任何參數也一樣。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `sa` 登入的登入識別碼。  
  
```  
SELECT SUSER_ID('sa');  
```  
  
## <a name="see-also"></a>請參閱＜  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [SUSER_SID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [系統函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
