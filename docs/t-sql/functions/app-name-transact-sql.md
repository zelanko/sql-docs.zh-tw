---
title: APP_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a6bb367cd82ca52e50b6ce6f79d7d0d4897f81ab
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="appname-transact-sql"></a>APP_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

函數，傳回目前工作階段的應用程式名稱 (如果應用程式設定名稱值)。
  
> [!IMPORTANT]  
>  用戶端提供應用程式名稱，且該應用程式名稱值未以任何方式驗證。 請勿在安全性檢查的任何環節中使用 **APP_NAME**。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
  
APP_NAME  ( )  
```  
  
## <a name="return-types"></a>傳回類型  
**nvarchar(128)**
  
## <a name="remarks"></a>Remarks  
使用 **APP_NAME** 來區別不同的應用程式，作為針對那些應用程式執行不同動作的方法。 例如，**APP_NAME** 可以區別不同的應用程式，以允許每個應用程式使用不同的日期格式。 它也可允許傳回到特定應用程式的參考資訊。
  
若要在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中設定應用程式名稱，請在 [連線到資料庫引擎] 對話方塊中按一下 [選項]。 在 [Additional Connection Parameters] (其他連線參數) 索引標籤中，以 `;app='application_name'` 格式提供 **app** 屬性
  
## <a name="example"></a>範例  
此範例檢查起始此處理序的用戶端應用程式是否為 `SQL Server Management Studio` 工作階段，並提供 US 或 ANSI 格式的日期。
  
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
[系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
[函數](../../t-sql/functions/functions.md)
  
  
