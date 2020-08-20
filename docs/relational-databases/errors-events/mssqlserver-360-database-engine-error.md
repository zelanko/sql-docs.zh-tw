---
description: MSSQLSERVER_360
title: MSSQLSERVER_360 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 360 (Database Engine error)
ms.assetid: e2b7c1b2-3679-4206-9b25-6bd55ef96a2c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 81b33aec71484900aa9dbb03826b146bdbdc209c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456160"
---
# <a name="mssqlserver_360"></a>MSSQLSERVER_360
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|360|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DML_UPDATE_SPARSE_AND_COLSET|  
|訊息文字|INSERT、UPDATE 或 MERGE 陳述式的目標資料行清單中不可以同時包含疏鬆資料行和內含疏鬆資料行的資料行集。 請重寫陳述式，以包含疏鬆資料行或資料行集，而非同時包含兩者。|  
  
## <a name="explanation"></a>說明  
資料行集是不具類型的 XML 表示，可將資料表的某些資料行結合到結構化輸出中。 嘗試修改此資料行集以及此資料行集中所含的資料行，造成兩個項目參考相同的資料行。  
  
## <a name="user-action"></a>使用者動作  
請重寫陳述式，以包含對此資料行或資料行集的參考，但不要將這兩個參考同時包含在陳述式內。  
  
