---
title: MSSQLSERVER_8525 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: "8525"
helpviewer_keywords: 8525 (Database Engine error)
ms.assetid: 297867c1-691e-4d6b-a3be-a7575015ecfa
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 91bca9f8deaa9af2caa9f17f6db307eee4cbe86f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver8525"></a>MSSQLSERVER_8525
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|8525|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|分散式交易完成。 請在新的交易或是 NULL 交易中編列這個工作階段。|  
  
## <a name="explanation"></a>說明  
在將分散式交易協調器搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一起使用的程式設計模型中，應用程式必須明確編列至分散式交易，並從分散式交易脫離。  
  
當符合下列四個條件時，就會發生此錯誤：  
  
-   應用程式已編列到分散式交易中。  
  
-   因為某種原因，交易已結束 (已認可或已回復)。  
  
-   使用者應用程式尚未明確脫離分散式交易，或尚未明確編列到新的分散式交易中。  
  
-   應用程式嘗試進行脫離現有分散式交易或編列到新的分散式交易以外的其他任何作業，例如發出查詢或啟動本機交易。  
  
當應用程式執行建立本機交易的作業時，會使用錯誤狀態 1，而當應用程式嘗試編列到繫結工作階段時，則會使用狀態 2。  
  
## <a name="user-action"></a>使用者動作  
在應用程式編列到分散式交易之後，應用程式必須明確脫離該分散式交易或編列到另一個分散式交易。 這個動作會隱含脫離先前編列的交易。 如需脫離或編列到分散式交易的正確語法，請參閱應用程式的程式設計介面手冊。  
  
