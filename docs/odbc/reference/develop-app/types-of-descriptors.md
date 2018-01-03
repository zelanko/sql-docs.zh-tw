---
title: "類型的描述元 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: descriptors [ODBC], types
ms.assetid: ec20e446-e540-41ad-8559-d9c0a5b8358f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9a5d5caf63abd6b9800ee6e65b7f6c30de108703
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="types-of-descriptors"></a>類型的描述元
描述元用來描述下列其中一項：  
  
-   一組零或多個參數。 參數描述元可以用來描述：  
  
    -   *應用程式的參數緩衝區*其中包含可能是輸入動態引數所設定的應用程式或執行的動態引數輸出**呼叫**SQL 陳述式。  
  
    -   *實作參數緩衝區*。 為輸入的動態引數，這可以包含相同的引數的應用程式的參數緩衝區之後應用程式可能會指定任何資料轉換。 對於輸出動態引數，這包含應用程式可能會指定任何資料轉換前的傳回引數。  
  
     為輸入的動態引數，應用程式必須運作的應用程式參數描述項，然後再執行任何 SQL 陳述式包含動態參數標記。 輸入和輸出動態引數，應用程式可以指定在實作參數描述元中的不同資料類型，以達到資料轉換。  
  
-   資料庫資料的單一資料列。 資料列描述項可以用來描述：  
  
    -   *實作資料列緩衝區，*其中包含從資料庫的資料列。 （這些緩衝區在概念上包含資料，在寫入或從資料庫讀取。 不過，未指定資料庫資料的預存的形式。 資料庫無法執行其他轉換來自其形式實作緩衝區中的資料）。  
  
    -   *應用程式的資料列緩衝區*呈現給應用程式，下列應用程式可能會指定任何資料轉換，其中會包含一個資料列。  
  
     應用程式上運作的應用程式的資料列描述項在任何情況下必須在應用程式變數中會顯示資料庫中的資料行資料。 若要達到資料轉換的資料行的資料，應用程式可以指定不同的資料類型與實作資料列描述項。  
  
 下表摘要說明描述元類型。  
  
|緩衝區類型|資料列|動態參數|  
|-----------------|----------|------------------------|  
|**應用程式緩衝區**|應用程式資料列描述項 (ARD)|應用程式參數描述項 (APD)|  
|**實作緩衝區**|實作資料列描述項 (IRD)|實作參數描述項 (IPD)|  
  
 參數或資料列緩衝區中，如果應用程式指定不同的資料類型中對應記錄的實作和應用程式的描述元，驅動程式會執行資料轉換時它會使用描述元。 例如，它可能會將數值和日期時間值轉換成字元字串格式。 (如有效轉換，請參閱[附錄 d： 資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)  
  
 描述元可以執行不同的角色。 不同的陳述式可以共用應用程式明確配置任何描述項。 在單一陳述式的資料列描述項可做為另一個陳述式中的參數描述元。  
  
 一律得知給定的描述元是否為應用程式描述項或實作描述項，即使描述元尚未使用的資料庫作業中。 實作會實作隱含地配置描述元，針對記錄預先定義的資料列，相對於陳述式控制代碼。 藉由呼叫的應用程式會配置任何描述項**SQLAllocHandle**是應用程式描述項。
