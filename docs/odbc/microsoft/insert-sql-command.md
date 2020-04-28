---
title: INSERT-SQL 命令 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300001"
---
# <a name="insert---sql-command"></a>INSERT - SQL 命令
將記錄附加至包含指定域值之資料表的結尾。  
  
 Visual FoxPro ODBC 驅動程式支援此命令的原生 Visual FoxPro 語言語法。 如需驅動程式特定的資訊，請參閱備註。  
  
## <a name="syntax"></a>語法  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>引數  
 插入*dbf_name*  
 指定要附加新記錄之資料表的名稱。 *dbf_name*可以包含路徑，而且可以是名稱運算式。  
  
 如果您指定的資料表未開啟，它會在新的工作區中以獨佔方式開啟，而新的記錄會附加到資料表。 未選取新的工作區;目前的工作區仍為選取狀態。  
  
 如果您指定的資料表是開啟的，INSERT 會將新記錄附加至資料表。 如果資料表是在目前工作區以外的工作區域中開啟，則在附加記錄之後，不會選取該資料表;目前的工作區仍為選取狀態。  
  
 [（ *fname1*[， *fname2*[，...]]）]  
 在新記錄中指定要插入值之欄位的名稱。  
  
 VALUES （ *eExpression1*[， *eExpression2*[，...]]）  
 指定插入新記錄的域值。 如果您省略功能變數名稱，則必須依照資料表結構所定義的順序來指定域值。  
  
## <a name="remarks"></a>備註  
 新記錄包含 VALUES 子句中列出的資料。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式將 ODBC SQL 語句插入傳送至資料來源時，Visual FoxPro ODBC 驅動程式會將命令轉換成 Visual FoxProINSERT 命令，而不會轉譯。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TABLE-SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
