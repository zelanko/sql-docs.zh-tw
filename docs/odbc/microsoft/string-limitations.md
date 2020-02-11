---
title: 字串限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7faab41bd52397ac0d352e04a9ec153571e93f1e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948766"
---
# <a name="string-limitations"></a>字串限制
SQL 語句字串的最大長度為65000個字元。  
  
 使用 Microsoft Access 驅動程式時，只支援 SQL-92 字串常數（使用單引號，而不是雙引號）。  
  
 不能在字串中使用管道字元（&#124;），不論該字元是否以反引號括住。  
  
 為了達到最大的互通性，應用程式應該在參數中傳遞字串，而不是傳遞引號的字串。
