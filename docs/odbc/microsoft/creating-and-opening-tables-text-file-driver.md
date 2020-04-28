---
title: 建立和開啟資料表（文字檔驅動程式） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280918"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>建立和開啟資料表 (文字檔驅動程式)
使用文字驅動程式時，會使用 Odbcinst 中指定的格式來建立新的資料表。 如果未指定，則會以 CSVDELIMITED 格式建立資料表。 根據預設，整數資料行預設為11個字元，而 FLOAT 資料行的預設值為22個字元。 日期資料行使用 YYYY-MM-DD 格式。 CHAR 和 LONGCHAR 資料行是 CREATE 語句中所指定的寬度。
