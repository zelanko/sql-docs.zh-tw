---
title: 相互關聯名稱 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- correlation names [ODBC]
- SQL grammar [ODBC], correlation names
ms.assetid: 76c36c6f-f8e1-4ece-a77b-611dde3bdd8a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b8a253f9d252beb42080d2085adb962206ebd94
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232314"
---
# <a name="correlation-names"></a>相互關聯名稱
完全支援相互關聯名稱，包括在資料表清單中。 例如，在下列字串中，E1 是名為 Emp 資料表相互關聯名稱：  
  
```  
SELECT * FROM Emp E1   
WHERE E1.LastName = 'Smith'  
```
