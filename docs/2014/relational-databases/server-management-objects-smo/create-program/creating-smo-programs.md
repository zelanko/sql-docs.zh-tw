---
title: 建立 SMO 程式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual Basic [SMO]
- Visual C# [SMO]
- programming [SMO]
- SQL Server Management Objects, programming
- SMO [SQL Server], programming
ms.assetid: 7d2f0bcf-f1ae-45b8-bc3f-7aea4fae7e45
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ccf26cf30c53e3a336e842cbbffc1ff517075fef
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52807840"
---
# <a name="creating-smo-programs"></a>建立 SMO 程式
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理物件 (SMO) 物件的一般程式設計包括所有物件共用的共同區域，例如，執行方法、設定屬性與操作集合。  
  
|主題|描述|  
|-----------|-----------------|  
|[連接到 SQL Server 的執行個體](connecting-to-an-instance-of-sql-server.md)|建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體連接的最基本 SMO 程式。 示範 Windows 驗證和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證。 同時包含示範連接到本機和遠端 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的範例。|  
|[從 SQL Server 的執行個體中斷連接](disconnecting-from-an-instance-of-sql-server.md)|示範如何從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體中斷連接的程式。|  
|[呼叫方法](calling-methods.md)|本節描述呼叫方法的一般方法。 示範參數的使用，以及如何處理在 <xref:System.Data.DataTable> 物件中傳回之資料的資料表。 同時包含如何呼叫物件建構函式以及如何呼叫 `Clone` 方法的範例。|  
|[設定屬性](setting-properties-smo.md)|本節描述如何設定不同類型的屬性。 示範如何設定和取得物件屬性。 同時包含建立物件時設定物件屬性，以及如何反覆運算物件所有屬性的範例。|  
|[使用集合](using-collections.md)|討論與物件集合搭配使用之技術的各種程式。 示範如何使用集合參考物件。 同時包含如何反覆運算集合成員的範例。|  
|[處理 SMO 事件](handling-smo-events.md)|本節描述如何在 SMO 中設定與處理事件。 包含如何設定事件處理常式，以及如何設定事件訂閱的範例。|  
|[處理 SMO 例外狀況](handling-smo-exceptions.md)|本節描述如何在 SMO 中設陷例外。 包含如何捕捉例外狀況，以及如何顯示內部例外狀況:的範例。|  
|[使用資料類型](working-with-data-types.md)|本節描述如何使用不同的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。 描述如何使用物件建構函式中的規格建構 datatype。 同時包含如何使用預設建構函式建立 datatype 的範例。|  
|[使用交易](using-transactions.md)|本節描述如何在 SMO 程式中實作交易處理。 包含如何在 SMO 程式中使用交易的範例。|  
|[使用擷取模式](using-capture-mode.md)|本節描述如何記錄 SMO 程式的輸出。 此範例會將 SMO 程式記錄為傳送到 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 執行個體以便稍後執行的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 陳述式。|  
  
  
