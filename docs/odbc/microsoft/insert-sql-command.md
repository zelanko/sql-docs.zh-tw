---
title: "插入的 SQL 命令 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: INSERT [ODBC]
ms.assetid: 9b648198-349f-46f6-b869-13d129945971
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4256908ef2b62fb75ff28f381d036caf2a72cdcd
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="insert---sql-command"></a>插入的 SQL 命令
將記錄附加至資料表，其中包含指定的欄位值的結尾。  
  
 Visual FoxPro ODBC 驅動程式支援的原生 Visual FoxPro 語言語法，此命令。 驅動程式特定資訊，請參閱 < 備註 >。  
  
## <a name="syntax"></a>語法  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>引數  
 INSERT INTO *dbf_name*  
 指定附加新的記錄資料表的名稱。 *dbf_name*可包含路徑和名稱的運算式。  
  
 如果您指定的資料表尚未開啟，新的工作區中，以獨佔方式開啟，且新的記錄會附加到資料表。 未選取新的工作區;目前的工作區仍為選取狀態。  
  
 如果您指定的資料表開啟時，INSERT 會將新的記錄附加至資料表。 如果資料表是在工作區中開啟的除了目前的工作區，它不被選取附加的記錄; 之後目前的工作區仍為選取狀態。  
  
 [( *fname1*[， *fname2*[，...]])]  
 指定新記錄中欄位的名稱到所插入的值。  
  
 值 ( *eExpression1*[， *eExpression2*[，...]])  
 指定插入新記錄的欄位值。 如果您省略欄位名稱，您必須指定欄位值的資料表結構所定義的順序。  
  
## <a name="remarks"></a>備註  
 新的記錄包含 VALUES 子句中所列的資料。  
  
## <a name="driver-remarks"></a>驅動程式註解  
 當您的應用程式傳送 ODBC SQL 陳述式插入至資料來源時，Visual FoxPro ODBC 驅動程式會將命令轉換成 Visual FoxProINSERT 命令，而不需轉譯中。  
  
## <a name="see-also"></a>請參閱＜  
 [建立資料表的 SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
