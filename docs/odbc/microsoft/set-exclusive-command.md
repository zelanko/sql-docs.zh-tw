---
title: 設定獨佔命令 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071763"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE 命令
指定是否要在網路上開啟資料表檔案以供獨佔或共用使用。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 限制在網路上開啟的資料表對開啟它的使用者的可存取性。 此資料表無法供網路上的其他使用者存取。 [設定獨佔] 也會防止所有其他使用者擁有唯讀存取權。  
  
 OFF  
 （驅動程式的預設值; 針對全域資料會話，Visual FoxPro 的預設值是 ON，私用資料會話則為 OFF）。允許在網路上開啟的資料表，由網路上的任何使用者共用及修改。  
  
## <a name="remarks"></a>備註  
 變更 [設定獨佔] 的設定並不會變更先前開啟之資料表的狀態。 例如，如果資料表是以 SET EXCLUSIVE 設定為 ON 來開啟，而 SET EXCLUSIVE 稍後變更為 OFF，則資料表會保留其獨佔使用狀態。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC Visual FoxPro 設定對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
