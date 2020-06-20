---
title: 第3課：使用 dta 命令提示字元公用程式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 30f27f4d-8852-4b12-ba62-57f63e496f1d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4a426dc282ffd052370e5c80c73b32b3f5051dc4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011557"
---
# <a name="lesson-3-using-the-dta-command-prompt-utility"></a>第 3 課：使用 dta 命令提示字元公用程式
  除了 Database Engine Tuning Advisor 所提供的功能，**dta** 命令提示字元公用程式還提供額外的功能。  
  
 您可以利用您愛用的 XML 工具和 Database Engine Tuning Advisor XML 結構描述來建立這個公用程式的輸入檔。 這個結構描述會在您安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時一併安裝，並且位於：C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd。  
  
 您也可以透過 [Microsoft 網站](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)，線上取得 Database Engine Tuning Advisor XML 結構描述。  
  
 在微調選項的設定上，Database Engine Tuning Advisor XML 結構描述非常靈活。 例如，它可讓您進行「假設」分析。 「假設」分析包括針對您要微調的資料庫來指定一組現有的實體設計結構和假設的實體設計結構，再利用 Database Engine Tuning Advisor 來分析它，以了解這個假設的實體設計是否能改進查詢處理效能。 這類分析的好處是既能夠評估新的組態，又免除了實際實作的負擔。 如果假設的實體設計所改進的效能不符需求，您很容易改變它，再分析它，直到產生的結果符合需求的組態出現為止。  
  
 此外，在使用 Database Engine Tuning Advisor XML 結構描述和 **dta** 命令提示字元公用程式時，您也可以將 Database Engine Tuning Advisor 功能納入指令碼中，再搭配其他資料庫設計工具來使用它。  
  
 如何使用 Database Engine Tuning Advisor 的 XML 輸入功能不在這個課程的範圍內。  
  
 這個課程介紹基本的 **dta** 命令提示字元公用程式語法、存取說明的方法，以及微調簡單工作負載的練習。  
  
 它包含下列主題：  
  
-   啟動**dta**命令提示字元公用程式和微調工作負載  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [啟動 dta 命令提示字元公用程式和微調工作負載](lesson-1-1-tuning-a-workload.md)  
  
  
