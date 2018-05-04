---
title: 相互關聯名稱 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- correlation names [ODBC]
- SQL grammar [ODBC], correlation names
ms.assetid: 76c36c6f-f8e1-4ece-a77b-611dde3bdd8a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0451d231f6d157c32c001c34e5faa20ea8ec80be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="correlation-names"></a>相互關聯名稱
完全支援相互關聯名稱，包括資料表清單中。 例如，下列字串中 E1 是名為 Emp 資料表相互關聯名稱：  
  
```  
SELECT * FROM Emp E1   
WHERE E1.LastName = 'Smith'  
```
