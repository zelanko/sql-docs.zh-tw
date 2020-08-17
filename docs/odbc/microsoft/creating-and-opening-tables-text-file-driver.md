---
description: 建立和開啟資料表 (文字檔驅動程式)
title: 建立和開啟 (文字檔驅動程式的資料表) |Microsoft Docs
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
ms.openlocfilehash: c64f74270e8c2bbf4645f72406113e88948d0da9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340964"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>建立和開啟資料表 (文字檔驅動程式)
使用文字驅動程式時，會使用 Odbcinst.ini 中指定的格式來建立新的資料表。 如果未指定，則會以 CSVDELIMITED 格式建立資料表。 根據預設，整數資料行預設為11個字元，而 FLOAT 資料行預設為22個字元。 日期資料行使用 YYYY-MM-DD 格式。 CHAR 和 LONGCHAR 資料行是 CREATE 語句中指定的寬度。
