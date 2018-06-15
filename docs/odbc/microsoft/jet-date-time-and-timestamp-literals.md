---
title: Jet： 日期、 時間和時間戳記常值 |Microsoft 文件
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
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 25064ec8edc48f99c1e68cd7df7a728ffa7673de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32898963"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet： 日期、 時間和時間戳記常值
最大的互通性，應用程式應該傳遞日期常值中使用逸出子句語法的 ODBC 標準格式：  
  
-   日期常值，{d '*值*'}，其中*宣告*e 是"yyyy-mm-dd"形式  
  
-   時間常值，{t '*值*'}，其中*宣告*e 是格式為"hh: mm:"  
  
 時間戳記常值 {ts'*值*'}，其中*宣告*e 的格式為"yyyy-mm-dd hh: mm: [.f...]"。
