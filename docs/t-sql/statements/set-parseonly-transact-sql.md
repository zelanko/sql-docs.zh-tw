---
title: "SET PARSEONLY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PARSEONLY_TSQL
- SET_PARSEONLY_TSQL
- PARSEONLY
- SET PARSEONLY
dev_langs:
- TSQL
helpviewer_keywords:
- parsing [SQL Server], SET PARSEONLY statement
- checking syntax
- PARSEONLY option
- syntax [SQL Server], verifying
- verifying syntax
- SET PARSEONLY statement
ms.assetid: 514ab042-c53e-4d96-be71-fb08fcc6ef3c
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2a117e81d9645edd9f24702ac01d8eeea3765726
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="set-parseonly-transact-sql"></a>SET PARSEONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  檢查每個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的語法，且會在未編譯或執行陳述式的情況下，傳回任何錯誤訊息。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SET PARSEONLY { ON | OFF }  
```  
  
## <a name="remarks"></a>備註  
 當 SET PARSEONLY 是 ON 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只會剖析陳述式。 當 SET PARSEONLY 是 OFF 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會編譯和執行陳述式。  
  
 SET PARSEONLY 的設定是在剖析階段進行設定，而不是在執行階段進行設定。  
  
 請勿在預存程序或觸發程序中使用 PARSEONLY。 如果 OFFSETS 選項是 ON，或未發生任何錯誤，SET PARSEONLY 會傳回位移。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [設定位移 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-offsets-transact-sql.md)  
  
  

