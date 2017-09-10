---
title: "（反斜線）(TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- '\_TSQL'
- '\'
dev_langs:
- TSQL
helpviewer_keywords:
- backwhack
- backslash
- excape character
- hack character
- '\ (backslash)'
- backslant
- bash
- reverse slant
- slosh
- reversed virgule
- line continuation character
- reverse solidus
ms.assetid: c97fbb20-3d12-4d0b-9b52-62a229bc83c0
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 011025d20b6341b9fa43b25f6c14c91a135a6ffa
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-utilities-statements---backslash"></a>SQL Server 公用程式陳述式的反斜線
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供的命令不[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式，但是會辨識**sqlcmd**和**osql**公用程式和[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]程式碼編輯器。 這些命令可用來簡化批次和指令碼的可讀性與執行。  
  
\ 中斷長的字串常數分成兩個或多個行來提高可讀性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
<first section of string> \  
<continued section of string>  
```  
  
## <a name="arguments"></a>引數  
 \<字串的第一個區段 >  
 這是字串的開頭。  
  
 \<繼續執行字串的區段 >  
 這是字串的接續。  
  
## <a name="remarks"></a>備註  
 這個命令會將字串的第一個區段和接續區段當做一個字串傳回，但不含反斜線。  
  
 反斜線不是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式， 它是可辨識的命令**sqlcmd**和**osql**公用程式和[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]程式碼編輯器。  
  
## <a name="examples"></a>範例  
 下列範例會使用反斜線和歸位字元，將字串分成兩行。  
  
```  
SELECT 'abc\  
def' AS ColumnResult;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 abcdef
 ```    
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [&#40; 除以 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/divide-transact-sql.md)   
 [&#40; 除 EQUALS &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [複合運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  

