---
title: Jet：日期、時間和時間戳記常值 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bb7f0fb02049b6d2f1897c4f495035aee2858f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085489"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet：日期、時間和時間戳記常值
為了達到最大的互通性，應用程式應該使用 escape 子句語法，傳遞 ODBC 標準格式的日期常值：  
  
-   若為日期常值，{d '*value*'}，其中*宣告*e 的格式為 "yyyy-mm-dd"  
  
-   若為時間常值，{t '*value*'}，其中*宣告*e 的格式為 "hh： mm： ss"  
  
 針對時間戳記常值 {ts '*value*'}，其中*宣告*e 的格式為 "yyyy-mm-dd hh： mm： ss [. f ...]"。
