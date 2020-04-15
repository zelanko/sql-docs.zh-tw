---
title: 過程呼叫 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32617cdb753f5fc1b9c52520cb609d2902137b54
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290769"
---
# <a name="procedure-invocation"></a>程序引動過程
使用 Microsoft Access 驅動程式時,可以使用**SQLExecDirect**或**SQLPrepare**函數使用具有以下語法,從驅動程式調用過程:[CALL*過程名稱*](*參數*[,*參數*]...)]。 請注意,表達式不支持作為調用過程的參數。  
  
 如果過程名稱包含破折號,則必須使用回引號 (『) 分隔名稱。  
  
 可以使用前面的語句調用參數化查詢。
