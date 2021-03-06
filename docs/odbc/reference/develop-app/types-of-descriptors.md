---
description: 描述項的類型
title: 描述項的類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], types
ms.assetid: ec20e446-e540-41ad-8559-d9c0a5b8358f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ef6bcaa737e26a4a3125e980f6f6bf3c3cff070
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491343"
---
# <a name="types-of-descriptors"></a>描述項的類型
描述項可用來描述下列其中一項：  
  
-   零或多個參數的集合。 參數描述元可以用來描述：  
  
    -   *應用程式參數緩衝區，* 其中包含應用程式所設定的輸入動態引數，或在執行 SQL 的**CALL**語句之後，輸出動態引數。  
  
    -   *實參數緩衝區*。 針對輸入動態引數，這會在應用程式可指定的任何資料轉換之後，包含與應用程式參數緩衝區相同的引數。 針對輸出動態引數，這會在應用程式可指定的任何資料轉換之前，包含傳回的引數。  
  
     針對輸入動態引數，應用程式必須在應用程式參數描述項上運作，才能執行任何包含動態參數標記的 SQL 語句。 針對輸入和輸出動態引數，應用程式可以從實參數描述元中指定不同的資料類型，以達成資料轉換。  
  
-   資料庫資料的單一資料列。 您可以使用資料列描述項來描述：  
  
    -   *執行資料列緩衝區，* 其中包含資料庫中的資料列。  (這些緩衝區在概念上包含了資料庫所寫入或讀取的資料。 但是，不會指定資料庫資料的預存形式。 資料庫可以從其在執行緩衝區中的表單上執行其他轉換。 )   
  
    -   應用程式資料 *列緩衝區，* 其中包含顯示給應用程式的資料列，並遵循應用程式可能指定的任何資料轉換。  
  
     如果資料庫中的資料行資料必須出現在應用程式變數中，則應用程式會在應用程式資料列描述項上運作。 若要達到資料行資料的資料轉換，應用程式可以從實資料列描述項中指定不同的資料類型。  
  
 下表摘要說明描述元類型。  
  
|緩衝區類型|資料列|動態參數|  
|-----------------|----------|------------------------|  
|**應用程式緩衝區**|應用程式資料列描述元 (ARD) |應用程式參數描述項 (APD) |  
|**執行緩衝區**|IRD) 的實資料列描述元 (| (IPD) 的實參數描述項|  
  
 針對參數或資料列緩衝區，如果應用程式在執行與應用程式描述項的對應記錄中指定不同的資料類型，則驅動程式會在使用描述項時執行資料轉換。 例如，它可能會將數值和日期時間值轉換成字元字串格式。  (如需有效的轉換，請參閱 [附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。 )   
  
 描述項可以執行不同的角色。 不同的語句可以共用應用程式明確配置的任何描述項。 一個語句中的資料列描述項可以做為另一個語句中的參數描述項。  
  
 無論指定的描述項是否為應用程式描述項或執行描述項，一律會知道指定的描述元是否為應用程式描述項或實描述項，即使尚未在資料庫作業中使用描述元 對於執行隱含配置的描述元，此實作為會記錄相對於語句控制碼的預先定義資料列。 應用程式透過呼叫 **SQLAllocHandle** 所配置的任何描述項都是應用程式描述項。
