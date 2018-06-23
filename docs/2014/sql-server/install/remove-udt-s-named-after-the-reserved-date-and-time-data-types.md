---
title: 移除 UDT&#39;保留的日期和時間資料類型命名 s |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- time data type [SQL Server], UDTs
- date data type [SQL Server], UDTs
ms.assetid: 48f109af-b1d1-4f03-a7e3-8a0b05ed94e8
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 71576529890a7cbc6da28e9a04566991d4e91b50
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133858"
---
# <a name="remove-udt39s-named-after-the-reserved-date-and-time-data-types"></a>移除 UDT&#39;s 名為保留的日期和時間資料類型
  Upgrade Advisor 偵測到依據針對 `date` 或 `time` 資料類型保留之詞彙所命名的使用者定義型別 (UDT)。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 用於資料類型的詞彙不應該當做 Common Language Runtime (CLR) 或別名 UDT 的名稱使用。  
  
## <a name="corrective-action"></a>更正動作  
 請移除依據此資料類型所命名的 UDT，然後使用未保留的名稱重新建立 UDT。  
  
  