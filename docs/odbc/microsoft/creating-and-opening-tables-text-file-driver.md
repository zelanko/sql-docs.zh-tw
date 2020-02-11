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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b36c02d772682088a799cfca66f5bbf3e169a67f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096537"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>建立和開啟資料表 (文字檔驅動程式)
使用文字驅動程式時，會使用 Odbcinst 中指定的格式來建立新的資料表。 如果未指定，則會以 CSVDELIMITED 格式建立資料表。 根據預設，整數資料行預設為11個字元，而 FLOAT 資料行的預設值為22個字元。 日期資料行使用 YYYY-MM-DD 格式。 CHAR 和 LONGCHAR 資料行是 CREATE 語句中所指定的寬度。
