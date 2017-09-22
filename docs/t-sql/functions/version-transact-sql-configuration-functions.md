---
title: "@@VERSION (TRANSACT-SQL) |Microsoft 文件"
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
- '@@VERSION'
- '@@VERSION_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@VERSION function'
- current SQL Server installation information
- versions [SQL Server], @@VERSION
- processors [SQL Server], types
ms.assetid: 385ba80e-7c28-41a5-9cdb-5648f3785983
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: c9fc3634abc5ca23c96f46adf2a52881ee15c40c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40version---transact-sql-configuration-functions"></a>（& s) #x 40; & #x 40。版本-Transact SQL 設定函式
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回系統和建立資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的目前安裝的。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@VERSION  
```  
  
## <a name="return-types"></a>傳回類型  
 **nvarchar**  
  
## <a name="remarks"></a>備註  
 @@VERSION結果會以一個 nvarchar 字串。 您可以使用[SERVERPROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/serverproperty-transact-sql.md)函式來擷取個別的屬性值。  
  
 傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的下列資訊。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本  
  
-   處理器架構  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建置日期  
  
-   著作權聲明  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本  
  
-   作業系統版本  
  
 傳回 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 的下列資訊。  
  
-   版本 - "Windows Azure SQL Database"  
  
-   產品層級 - "(CTP)" 或 "(RTM)"  
  
-   產品版本  
  
-   建置日期  
  
-   著作權聲明  
  
## <a name="examples"></a>範例  
  
### <a name="a-return-the-current-version-of-includessnoversionincludesssnoversion-mdmd"></a>答： 傳回目前的版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 下列範例會顯示傳回目前安裝架構的版本資訊。  
  
```  
SELECT @@VERSION AS 'SQL Server Version';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-return-the-current-version-of-includessdwincludesssdw-mdmd"></a>B. 傳回目前的版本[!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
  
```  
SELECT @@VERSION AS 'SQL Server PDW Version';  
```  
  
## <a name="see-also"></a>另請參閱  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
  


