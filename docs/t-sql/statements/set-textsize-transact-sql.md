---
title: "SET TEXTSIZE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 04/12/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TEXTSIZE_TSQL
- TEXTSIZE
- SET_TEXTSIZE_TSQL
- SET TEXTSIZE
dev_langs:
- TSQL
helpviewer_keywords:
- SET TEXTSIZE statement
- SELECT statement [SQL Server], text size returned
- size [SQL Server], text and image data
- TEXTSIZE option
- text size returned [SQL Server]
ms.assetid: 787154a6-39a6-4dd6-a6d0-67b4364f95d5
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d9925b382a7d09722846ca7da583fb92fe4609c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="set-textsize-transact-sql"></a>SET TEXTSIZE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定的大小**varchar （max)**， **nvarchar （max)**， **varbinary （max)**，**文字**， **ntext**與**映像**SELECT 陳述式傳回的資料。  
  
> [!IMPORTANT]  
>  **ntext**，**文字**，和**映像**的未來版本將移除的資料型別[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請避免在新的開發工作中使用這些資料類型，並規劃修改目前在使用這些資料類型的應用程式。 請改用 **nvarchar(max)**、 **varchar(max)**和 **varbinary(max)** 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SET TEXTSIZE { number }   
```  
  
## <a name="arguments"></a>引數  
 *number*  
 長度**varchar （max)**， **nvarchar （max)**， **varbinary （max)**，**文字**， **ntext**，或**映像**資料，以位元組為單位。 *數字*是最大值 2147483647 (2 GB) 的整數。  值為-1 表示無限制的大小。 值為 0 會將大小重設為預設值為 4 KB。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client （10.0 和更新版本） 和 ODBC 驅動程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自動指定`-1`（無限制） 時連線。  
  
 **驅動程式超過[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者 （版本 9）[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接時，都會將 TEXTSIZE 設為 2147483647。  
  
## <a name="remarks"></a>備註  
 設定 SET TEXTSIZE 會影響 @@TEXTSIZE函式。  
  
 SET TEXTSIZE 的設定是在執行階段進行設定，而不是在剖析階段進行設定。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

