---
description: SET EXCLUSIVE 命令
title: 設定專屬命令 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 413c9188decc9011c2816b692b1fb4b6112ec45b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466350"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE 命令
指定是否在網路上針對專用或共用用途開啟資料表檔案。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 限制在網路上開啟之資料表對開啟它的使用者的可存取性。 網路上的其他使用者無法存取此資料表。 [設定專屬] 也會防止所有其他使用者擁有唯讀存取權。  
  
 OFF  
 驅動程式 (預設值;Visual FoxPro 的預設值適用于全域資料會話，而針對私用資料會話則為 OFF。 ) 允許網路上開啟的資料表可由網路上的任何使用者共用及修改。  
  
## <a name="remarks"></a>備註  
 變更 SET EXCLUSIVE 的設定不會變更先前開啟之資料表的狀態。 例如，如果資料表開啟時，將 SET EXCLUSIVE 設為 ON，而 SET EXCLUSIVE 則在稍後變更為 OFF，則資料表會保留其獨佔使用狀態。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC Visual FoxPro 設定對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
