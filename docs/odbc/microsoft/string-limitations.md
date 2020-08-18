---
description: 字串限制
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c21d86a3c626ced52c6b7915d3cfbd9322fb596e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449130"
---
# <a name="string-limitations"></a>字串限制
SQL 語句字串的長度上限為65000個字元。  
  
 使用 Microsoft Access 驅動程式時，僅支援以單引號括住的 SQL-92 字串 (常數，) 不支援雙引號。  
  
 無論字元是否以引號括住，不能在字串中使用管道字元 ( # A0) 。  
  
 為了達到最大的互通性，應用程式應該在參數中傳遞字串，而不是傳遞引號的字串。
