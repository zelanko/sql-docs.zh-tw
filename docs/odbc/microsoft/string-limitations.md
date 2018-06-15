---
title: 字串限制 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd397b02f72a9962e4fe87683141fa98f81cfbdc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32902653"
---
# <a name="string-limitations"></a>字串限制
SQL 陳述式字串的長度上限為 65000 個字元。  
  
 使用 Microsoft Access 驅動程式時，只有 SQL 92 字串常數 （使用單引號，不雙引號） 支援。  
  
 縱線字元 (&#124;) 不能在字串中，是否或不以回復括住的字元。  
  
 最大的互通性，應用程式應該傳遞字串參數，而不是傳遞加上引號的字串。
