---
title: 插入 - SQL 指令 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- INSERT [ODBC]
ms.assetid: 9b648198-349f-46f6-b869-13d129945971
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ce00005fb1aa0ca9732fc5e9cfeacd6faf6ef9e1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300001"
---
# <a name="insert---sql-command"></a>INSERT - SQL 命令
將記錄追加到包含指定欄位值的表的末尾。  
  
 Visual FoxPro ODBC 驅動程式支援此命令的本機 Visual FoxPro 語言文法。 有關特定於驅動程序的資訊,請參閱備註。  
  
## <a name="syntax"></a>語法  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>引數  
 插入*到dbf_name*  
 指定追加新記錄的表的名稱。 *dbf_name*可以包含路徑,也可以是名稱運算式。  
  
 如果指定的表未打開,則它將在新工作區中專門打開,並將新記錄追加到表中。 未選擇新工作區;未選擇新工作區。當前工作區保持選中狀態。  
  
 如果指定的表處於打開狀態,則 INSERT 將新記錄追加到表中。 如果表在當前工作區以外的工作區中打開,則在追加記錄后不會選擇該表;如果表在當前工作區以外的工作區域中打開,則不會選擇該表。當前工作區保持選中狀態。  
  
 *[(fname1*[, *fname2*[, .]) ]  
 在新記錄中指定插入值的欄位的名稱。  
  
 值 *(eExpression1*[, *eExpression2*], .*)  
 指定插入到新紀錄中的欄位值。 如果省略欄位名稱,則必須按表結構定義的順序指定欄位值。  
  
## <a name="remarks"></a>備註  
 新記錄包含 VALUE 子句中列出的數據。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當應用程式將 ODBC SQL 語句 INSERT 發送到資料來源時,Visual FoxPro ODBC 驅動程式將該命令轉換為 Visual FoxProINSERT 命令,無需翻譯。  
  
## <a name="see-also"></a>另請參閱  
 [建立表 - SQL 指令](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
