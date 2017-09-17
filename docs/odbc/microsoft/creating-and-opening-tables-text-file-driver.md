---
title: "建立及開啟資料表 （文字檔案驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 41190a0a3eabda2f73c8f6046a64b7b7db929fa1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="creating-and-opening-tables-text-file-driver"></a>建立及開啟資料表 （文字檔案驅動程式）
使用文字驅動程式時，會使用在 Odbcinst.ini 中指定的格式來建立新的資料表。 如果未指定，CSVDELIMITED 格式來建立資料表。 根據預設，預設為 11 個字元的整數資料行，浮點數資料行預設為 22 個字元。 日期資料行使用 YYYY MM DD 的格式。 CHAR 和 LONGCHAR 資料行是在 CREATE 陳述式中指定的寬度。
