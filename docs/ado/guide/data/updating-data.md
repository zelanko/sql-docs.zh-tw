---
title: "更新資料 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ADO], about data updates
- updating data [ADO], about updating data
ms.assetid: 6508e4e9-e33a-4dad-b340-5d632fd78a91
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 936808c28286f1d3bd3600b7c5240894bd952bf7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="updating-data"></a>更新資料
更新行為和功能主要是依據更新模式 （鎖定類型）、 資料指標類型，以及游標位置。  
  
 使用**更新**方法，以儲存您對目前記錄的任何變更**資料錄集**物件後呼叫**AddNew**方法，或自變更任何欄位值在現有的記錄。 **資料錄集**物件必須支援更新。  
  
 如果**資料錄集**物件支援批次更新，您可以快取多對一或多個記錄的變更在本機直到您呼叫**UpdateBatch**方法。 如果您正在編輯目前的記錄或加入新的記錄，當您呼叫**UpdateBatch**自動呼叫方法時，ADO 會**更新**方法來儲存目前的記錄之前的任何暫止的變更傳送給提供者的批次的變更。  
  
 目前的記錄會保留目前之後呼叫**更新**或**UpdateBatch**方法。  
  
 此章節包含下列主題。  
  
-   [即時模式](../../../ado/guide/data/immediate-mode.md)  
  
-   [批次模式](../../../ado/guide/data/batch-mode.md)  
  
-   [交易處理](../../../ado/guide/data/transaction-processing.md)
