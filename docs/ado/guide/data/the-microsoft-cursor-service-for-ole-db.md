---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aeac8c848f01f01e8969f94c571ad15f5e7f615a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923912"
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>適用於 OLE DB 的 Microsoft 資料指標服務
當您選取用戶端資料指標，或將**CursorLocation**屬性設定為**adUseClient**時，就會叫用 Microsoft cursor 服務來進行 OLE DB。 您也可能會看到「用戶端資料指標引擎」的參考，這在 ADO 的內容中基本上是相同的。 這項服務會補充資料提供者的資料指標支援函數。 因此，您可以觀察所有資料提供者的相對一致功能。  
  
 OLE DB 的資料指標服務可提供動態屬性，並增強某些方法的行為。 例如， **Optimize** dynamic 屬性可讓您建立暫存索引來加速特定作業，例如**Find**方法。  
  
 在所有情況下，資料指標服務都會啟用批次更新的支援。 它也會在資料提供者只能提供較不支援的資料指標（例如靜態資料指標）時，模擬更有能力的游標類型，例如動態資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [適用于 OLE DB 的 Microsoft 資料指標服務（ADO 服務元件）](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)
