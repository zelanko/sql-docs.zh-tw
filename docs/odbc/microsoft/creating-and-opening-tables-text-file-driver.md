---
title: "建立及開啟資料表 （文字檔案驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 65288e34df82aa6e37c8be04e3fd2aae7b57e472
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="creating-and-opening-tables-text-file-driver"></a>建立及開啟資料表 （文字檔案驅動程式）
使用文字驅動程式時，會使用在 Odbcinst.ini 中指定的格式來建立新的資料表。 如果未指定，CSVDELIMITED 格式來建立資料表。 根據預設，預設為 11 個字元的整數資料行，浮點數資料行預設為 22 個字元。 日期資料行使用 YYYY MM DD 的格式。 CHAR 和 LONGCHAR 資料行是在 CREATE 陳述式中指定的寬度。
