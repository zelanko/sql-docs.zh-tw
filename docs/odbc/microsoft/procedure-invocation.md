---
description: 程序引動過程
title: 程式調用 |Microsoft Docs
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
ms.openlocfilehash: e2643a36c834b577dfcecdcc81fd938a3a7d1018
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340444"
---
# <a name="procedure-invocation"></a>程序引動過程
使用 Microsoft Access 驅動程式時，您可以使用 **SQLExecDirect** 或 **SQLPrepare** 函式，以下列語法從驅動程式叫用程式： {CALL *procedure-name* [ (*parameter*[，*parameter*] ... ) ]}。 請注意，不支援將運算式做為呼叫之程式的參數。  
  
 如果程式名稱包含破折號，則名稱必須以後引號分隔 (') 。  
  
 您可以使用上一個語句來呼叫參數化查詢。
