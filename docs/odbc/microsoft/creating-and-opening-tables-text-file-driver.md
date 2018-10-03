---
title: 建立和開啟資料表 （文字檔驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce901e6a8639c8a2caea6e55cbaa18fedb56f4a7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769096"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>建立和開啟資料表 (文字檔驅動程式)
使用文字驅動程式時，會建立新的資料表，使用在 Odbcinst.ini 中指定的格式。 如果未指定，資料表會 CSVDELIMITED 格式。 根據預設，預設為 11 個字元的整數資料行，浮點數資料行預設為 22 個字元。 日期資料行使用 YYYY 為 YYYY-MM-DD 格式。 CHAR 和 LONGCHAR 資料行是在 CREATE 陳述式中指定的寬度。
