---
title: "APP_NAME (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- APP_NAME_TSQL
- APP_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- name checking for current session [SQL Server]
- sessions [SQL Server], application names
- applications [SQL Server], names
- current session application names
- APP_NAME function
ms.assetid: e491e192-9b30-4243-bc19-33c133fe08a8
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c4f63ae216bad0269415ac5e0aa57a7543500f0c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="appname-transact-sql"></a>APP_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回目前工作階段的應用程式名稱 (如果是由該應用程式所設定)。
  
> [!IMPORTANT]  
>  應用程式名稱由是用戶端所提供，而且未使用任何方式驗證。 請勿使用**APP_NAME**安全性檢查的一部分。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
  
APP_NAME  ( )  
```  
  
## <a name="return-types"></a>傳回類型  
**nvarchar （128)**
  
## <a name="remarks"></a>備註  
使用**APP_NAME**當您想要針對不同的應用程式中執行不同的動作。 例如，以不同方式為不同的應用程式格式化日期，或是將參考用訊息傳回某些應用程式。
  
若要設定應用程式名稱在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，請在**連接到 Database Engine**對話方塊中，按一下 **選項**。 在**其他連接參數**索引標籤上，提供**應用程式**格式屬性`;app='application_name'`
  
## <a name="examples"></a>範例  
下列範例會檢查起始此程序的用戶端應用程式是否為 `SQL Server Management Studio` 工作階段，並提供 US 或 ANSI 格式的日期。
  
```sql
USE AdventureWorks2012;  
GO  
IF APP_NAME() = 'Microsoft SQL Server Management Studio - Query'  
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 101) + '.';  
ELSE   
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 102) + '.';  
GO  
```  
  
## <a name="see-also"></a>另請參閱
[系統函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
[函數](../../t-sql/functions/functions.md)
  
  

