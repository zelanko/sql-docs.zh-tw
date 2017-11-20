---
title: "程序引動過程 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fd42836285c29e36e6bb64ebe594df570876ff6e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="procedure-invocation"></a>程序引動過程
使用 Microsoft Access 驅動程式時，程序可以叫用從驅動程式使用**SQLExecDirect**或**SQLPrepare**函式搭配下列語法: {呼叫*程序名稱* [(*參數*[，*參數*]...)]}。 請注意，做為參數，呼叫的程序不支援運算式。  
  
 如果程序名稱包含破折號，必須為反引號 （'） 分隔名稱。  
  
 參數化的查詢，可以使用前一個陳述式來呼叫。

