---
title: 程序呼叫 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290769"
---
# <a name="procedure-invocation"></a>程序引動過程
使用 Microsoft Access 驅動程式時，可以使用**SQLExecDirect**或**SQLPrepare**函式，透過下列語法從驅動程式叫用程式： {CALL *procedure-name* [（*parameter*[，*parameter*] ...）]}。 請注意，運算式不支援做為所呼叫程式的參數。  
  
 如果程式名稱包含破折號，名稱就必須以後引號（'）分隔。  
  
 參數化查詢可以使用先前的語句來呼叫。
