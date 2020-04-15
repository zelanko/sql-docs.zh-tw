---
title: SET 獨佔命令 |微軟文件
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
ms.openlocfilehash: d140c4be3ab850547ac82f9b954e7313b008dbf0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300858"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE 命令
指定表檔是打開,以便在網路上獨佔用途還是共用用途。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 將在網路上打開的表的可存取性限制為打開該表的使用者。 網路上的其他用戶無法訪問該表。 設置獨存打開還阻止所有其他使用者具有唯讀訪問許可權。  
  
 OFF  
 (驅動程式默認值;Visual FoxPro 的預設值為全域數據會話為"打開",對於私有數據會話為 OFF。允許網路上的任何使用者共用和修改在網路上打開的表。  
  
## <a name="remarks"></a>備註  
 更改 SET EXCLUSIVE 的設定不會更改以前打開的表的狀態。 例如,如果將具有 SET 獨佔集的表打開,然後將 SET 獨佔更改為 OFF,則該表將保留其獨佔使用狀態。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC Visual FoxPro 設定對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
