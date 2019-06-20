---
title: OLE DB 的 Microsoft 資料指標服務 |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: cbf289e73cd3cb94418521f3d4070cf155a7fdf2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704912"
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>適用於 OLE DB 的 Microsoft 資料指標服務
當您選取用戶端資料指標，或設定**CursorLocation**屬性設**adUseClient**，Microsoft 資料指標服務叫用的 OLE DB。 您也可能會看到 「 用戶端資料指標引擎 」，也就是基本上相同的 ADO 內容中的參考。 這項服務可補充資料提供者的資料指標支援函式。 如此一來，您能夠察覺相當一致的功能，從所有資料提供者。  
  
 OLE DB 資料指標服務提供動態屬性，並增強特定方法的行為。 例如，**最佳化**動態屬性可讓您建立暫存的索引，以利於進行某些作業，例如**尋找**方法。  
  
 資料指標服務可支援在所有情況下的批次更新。 資料提供者只可以提供效能較差的資料指標，例如靜態資料指標時，它也會模擬功能更強大的資料指標類型，例如動態資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB （ADO 服務元件） 的 Microsoft 資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)
