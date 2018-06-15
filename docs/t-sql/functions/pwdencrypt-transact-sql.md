---
title: PWDENCRYPT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PWDENCRYPT
- PWDENCRYPT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PWDENCRYPT function [Transact-SQL]
ms.assetid: 333e9a43-1099-4b9b-b941-4b0b016f47f3
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 974f09b3b98844b91a6ac339411d675c333b3fb6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33056175"
---
# <a name="pwdencrypt-transact-sql"></a>PWDENCRYPT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回輸入值的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 密碼雜湊，此輸入值使用目前版本的密碼雜湊演算法。  
  
 PWDENCRYPT 是比較舊的函數，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未來版本中可能不支援。 請改為使用 [HASHBYTES](../../t-sql/functions/hashbytes-transact-sql.md)。 HASHBYTES 提供更多雜湊演算法。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
PWDENCRYPT ( 'password' )  
```  
  
## <a name="arguments"></a>引數  
 *password*  
 這是要加密的密碼。 *password* 為 **sysname**。  
  
## <a name="return-types"></a>傳回類型  
 **varbinary(128)**  
  
## <a name="permissions"></a>Permissions  
 PWDENCRYPT 可以公開使用。  
  
## <a name="see-also"></a>另請參閱  
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [PWDCOMPARE &#40;Transact-SQL&#41;](../../t-sql/functions/pwdcompare-transact-sql.md)  
  
  
