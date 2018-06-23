---
title: 資料收集器程式設計 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data collector [SQL Server], programming
ms.assetid: 53b4752b-055d-4716-b2bc-75b4cce84101
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a9a3e4428eee6057ac3e38e553eec43616504a06
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144989"
---
# <a name="data-collector-programming"></a>資料收集器程式設計
  <xref:Microsoft.SqlServer.Management.Collector> 中的資料收集器 API 可透過物件模型，以程式設計的方式控制所有的組態作業。 此外，許多使用 API 的資料收集作業都會實作為安裝在伺服器上的預存程序。  
  
 下圖顯示資料收集器物件模型的重要元素。  
  
 ![資料收集器物件模型](../../../2014/database-engine/dev-guide/media/dc-objectmodel.gif "資料收集器物件模型")  
  
  