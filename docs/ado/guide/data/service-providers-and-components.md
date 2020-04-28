---
title: 服務提供者和元件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a78db07f5ba445c54108558b2ff222bd217c2bbe
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924249"
---
# <a name="service-providers-and-components"></a>服務提供者和元件
服務提供者是一種元件，可執行資料存放區原本不支援的擴充介面，藉此擴充資料提供者的功能。  
  
 通用資料存取提供一個*元件架構*，可讓個別的特製化元件在不支援的存放區上，執行一組離散的資料庫功能或「服務」。 因此，而不是強迫每個資料存放區提供自己的擴充功能，或強制泛型應用程式在內部執行資料庫功能，服務元件會提供一個通用的執行方式，供任何應用程式在存取任何資料存放區時使用。 事實上，某些功能是由資料存放區以原生方式實作為，而有些則是透過泛型元件，對應用程式而言是透明的。  
  
 例如，資料指標引擎（例如[OLE DB 的 Cursor 服務](https://msdn.microsoft.com/57638feb-4ecd-4051-becb-8f828d21cf44)）是一種服務元件，可以從連續、順向資料存放區取用資料，以產生可滾動的資料。 ADO 經常使用的其他服務提供者包括[microsoft OLE DB 持續性提供者（Ado 服務提供者）](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) 、適用于[OLE DB 的 Microsoft 資料成形服務（Ado 服務提供者）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) （適用于階層式**記錄集**），以及[MICROSOFT OLE DB 遠端處理提供者（ado 服務提供者）](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) （用於在遠端電腦上叫用資料提供者）。  
  
 如需服務和資料提供者的詳細資訊，請參閱[附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)。
