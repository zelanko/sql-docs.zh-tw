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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44e773248cd2d61e211f6de98d5a0f81acc78bd1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62471173"
---
# <a name="insert---sql-command"></a>INSERT - SQL 命令
將記錄附加至資料表，其中包含指定的欄位值的結尾。  
  
 Visual FoxPro ODBC Driver 支援原生 Visual FoxPro 語言語法，此命令。 驅動程式專屬資訊，請參閱 < 備註 >。  
  
## <a name="syntax"></a>語法  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>引數  
 INSERT INTO *dbf_name*  
 指定要附加新的記錄資料表的名稱。 *dbf_name*可以包含路徑，而且可以是名稱的運算式。  
  
 如果您指定的資料表尚未開啟，以獨佔方式在新的工作區中開啟，新的記錄會附加到資料表。 新的工作區不是選取狀態;目前的工作區仍為選取狀態。  
  
 如果您指定的資料表開啟時，INSERT 會將新記錄附加至資料表。 如果資料表是在工作區中開啟的除了目前的工作區，未選取附加記錄; 之後目前的工作區仍為選取狀態。  
  
 [( *fname1*[, *fname2*[, ...]])]  
 指定新記錄中欄位的名稱到所插入的值。  
  
 VALUES ( *eExpression1*[, *eExpression2*[, ...]])  
 指定插入新資料錄的欄位值。 如果您省略的欄位名稱，您必須指定欄位值的資料表結構所定義的順序。  
  
## <a name="remarks"></a>備註  
 新的記錄包含的 VALUES 子句中所列的資料。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式傳送至資料來源的 ODBC SQL 陳述式插入時，則 Visual FoxPro ODBC Driver 會將命令轉換 Visual FoxProINSERT 命令，無需進行翻譯。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TABLE-SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
