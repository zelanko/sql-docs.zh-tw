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
manager: craigg
ms.openlocfilehash: e4ae286264f4f896fe1b8a36d9c400367bd818dd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662424"
---
# <a name="service-providers-and-components"></a>服務提供者和元件
服務提供者是藉由實作擴充原生不支援資料存放區的介面中擴充的資料提供者功能的元件。  
  
 通用資料存取提供*元件架構*，可個別、 特製化的元件，才能實作離散組資料庫的功能或 「 服務 」，讓效能較差的存放區上。 因此，而不是強制執行每個資料存放區，以提供自己的擴充功能實作，或強制執行在內部實作的資料庫功能的泛型應用程式，服務元件，提供可以任何應用程式的一般實作存取任何資料存放區時，會使用它。 有些功能由資料存放區，以及一些透過一般的元件以原生方式實作的事實是向應用程式。  
  
 例如，資料指標引擎，例如[OLE DB 的資料指標服務](http://msdn.microsoft.com/57638feb-4ecd-4051-becb-8f828d21cf44)，是可從連續的順向的資料存放區來產生可捲動的資料使用資料的服務元件。 包含其他服務提供者，通常由 ADO [Microsoft OLE DB 持續性提供者 （ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) （適用於將資料儲存至檔案）， [Microsoft Data Shaping Service 的 OLE DB （ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (如階層**資料錄集**)，而[Microsoft OLE DB 遠端服務提供者 （ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) （適用於叫用遠端電腦上的資料提供者）。  
  
 如需有關服務和資料提供者的詳細資訊，請參閱[附錄 a： 提供者](../../../ado/guide/appendixes/appendix-a-providers.md)。
