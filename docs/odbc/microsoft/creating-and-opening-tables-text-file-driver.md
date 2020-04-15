---
title: 建立與開啟表(文字檔案驅動程式) |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae13312299f131d1957557db28bbe4db0bf7b4c7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280918"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>建立和開啟資料表 (文字檔驅動程式)
使用文字驅動程式時,將使用 Odbcinst.ini 中指定的格式創建新錶。 如果未指定,則以 CSVDELIMITED 格式建立表。 默認情況下,INTEGER 列預設為 11 個字元,FLOAT 列預設為 22 個字元。 日期列使用 YYYY-MM-DD 格式。 CHAR 和 LONGCHAR 列是 CREATE 語句中指定的寬度。
