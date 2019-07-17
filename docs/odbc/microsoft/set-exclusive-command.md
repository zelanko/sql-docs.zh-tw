---
title: SET EXCLUSIVE 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d1a37043d332b54d0d5c5ebb7b2ba9f3acce000
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071763"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE 命令
指定是否開啟資料表的檔案，以進行獨佔或共用網路上使用。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 ON  
 限制資料表，以開啟它的使用者在網路上開啟的協助的工具。 資料表不在網路上其他使用者可以存取。 SET EXCLUSIVE ON 也會防止所有其他使用者擁有唯讀存取權。  
  
 OFF  
 （預設驅動程式; Visual FoxPro 的預設值為 ON 的全域資料的工作階段和 OFF 的私用資料的工作階段）。可讓您在共用及修改任何使用者在網路上的網路上開啟的資料表。  
  
## <a name="remarks"></a>備註  
 變更設定專屬的設定不會變更狀態的先前開啟的資料表。 比方說，如果資料表以設定專屬設為 ON 來開啟並設定專屬稍後變更為 OFF，則資料表會保留其獨佔使用的狀態。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC Visual FoxPro 設定對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
