---
description: 適用於 OLE DB 的 Microsoft 資料指標服務
title: 適用于 OLE DB 的 Microsoft 資料指標服務 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursor service for ole db [ADO]
- cursors [ADO], cursor service for OLE DB
ms.assetid: 1ac3bd9b-2d45-4cc8-88ec-bd8a218cfb49
author: rothja
ms.author: jroth
ms.openlocfilehash: f3646ec86f76fcba2f6b82759a4784de7d463279
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452740"
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>適用於 OLE DB 的 Microsoft 資料指標服務
當您選取用戶端資料指標，或將 **CursorLocation** 屬性設定為 **adUseClient**時，您會叫用 Microsoft cursor Service 進行 OLE DB。 您也可能會看到「用戶端資料指標引擎」的參考，這基本上是 ADO 內容中的相同內容。 這項服務會補充資料提供者的資料指標支援功能。 如此一來，您就可以感知所有資料提供者的相對一致功能。  
  
 OLE DB 的資料指標服務可提供動態屬性，並增強某些方法的行為。 例如， **Optimize** 動態屬性可建立暫存索引來加速特定作業，例如 **Find** 方法。  
  
 在所有情況下，資料指標服務都可支援批次更新。 當資料提供者只能提供較小的資料指標（例如靜態資料指標）時，它也會模擬更有能力的資料指標類型，例如動態資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [適用于 OLE DB (ADO 服務元件的 Microsoft 資料指標服務) ](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)
