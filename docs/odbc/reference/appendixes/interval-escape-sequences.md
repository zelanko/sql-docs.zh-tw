---
description: 間隔逸出序列
title: 間隔 Escape 序列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2ef792403352568ce5f8d92c07a5b0e1027b507
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483291"
---
# <a name="interval-escape-sequences"></a>間隔逸出序列
ODBC 會針對間隔常值使用 escape 序列。 此 escape 順序的語法如下所示：  
  
 {*interval-常*值}  
  
 如需 *間隔常*值的 BNF 語法，請參閱本附錄稍後的「 [間隔常值語法](../../../odbc/reference/appendixes/interval-literal-syntax.md) 」一節。  
  
 如果資料來源支援間隔資料類型，則支援間隔常值 escape 序列。 應用程式應該呼叫 **SQLGetTypeInfo** 來判斷是否支援這些資料類型。
