---
description: 更新資料
title: 正在更新資料 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], about data updates
- updating data [ADO], about updating data
ms.assetid: 6508e4e9-e33a-4dad-b340-5d632fd78a91
author: rothja
ms.author: jroth
ms.openlocfilehash: 5ea884479e7353b822e8b679a0fff34d70c3fd93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452640"
---
# <a name="updating-data"></a>更新資料
更新行為和功能主要取決於更新模式 (鎖定類型) 、資料指標類型和資料指標位置。  
  
 使用 **Update** 方法，即可儲存您對 **記錄集** 物件的目前記錄所做的任何變更，因為呼叫 **AddNew** 方法，或變更現有記錄中的任何域值。 **記錄集**物件必須支援更新。  
  
 如果 **記錄集** 物件支援批次更新，您可以在本機快取一或多個記錄的多個變更，直到您呼叫 **UpdateBatch** 方法為止。 如果您要編輯目前的記錄，或在呼叫 **UpdateBatch** 方法時加入新的記錄，ADO 會自動呼叫 **Update** 方法，在將批次變更傳送給提供者之前，先將任何暫止的變更儲存至目前的記錄。  
  
 當您呼叫 **Update** 或 **UpdateBatch** 方法之後，目前的記錄仍保持最新狀態。  
  
 此章節包含下列主題。  
  
-   [即時模式](../../../ado/guide/data/immediate-mode.md)  
  
-   [批次模式](../../../ado/guide/data/batch-mode.md)  
  
-   [交易處理](../../../ado/guide/data/transaction-processing.md)
