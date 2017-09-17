---
title: "服務提供者和元件 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c8f574b00b5c53caef2184d2923e79746d3ef56c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="service-providers-and-components"></a>服務提供者和元件
服務提供者是藉由實作擴充的介面不會原生支援的資料存放區擴充的資料提供者功能的元件。  
  
 通用資料存取提供*元件架構*，可個別、 特製化的元件，以實作特定一組資料庫功能或 「 服務 」，讓較不支援的存放區之上。 因此，而不是強制執行每個資料存放區，以提供它自己的擴充功能的實作，或強制在內部實作的資料庫功能的泛型應用程式，服務元件，提供可以任何應用程式的一般實作存取任何資料存放區時使用。 某些功能由資料存放區，而某些一般的元件透過原生實作的事實是透明的應用程式。  
  
 例如，資料指標引擎，例如[OLE DB 的資料指標服務](http://msdn.microsoft.com/en-us/57638feb-4ecd-4051-becb-8f828d21cf44)，是一種服務元件，可使用循序的順向的資料存放區，以產生可捲動的資料的資料。 通常由 ADO 使用其他服務提供者包括[Microsoft OLE DB 持續性提供者 （ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) （適用於將資料儲存至檔案）， [Microsoft Data Shaping Service 的 OLE DB （ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (如階層式**資料錄集**)，而[Microsoft OLE DB 遠端服務提供者 （ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) （適用於叫用遠端電腦上的資料提供者）。  
  
 如需有關服務和資料提供者的詳細資訊，請參閱[附錄 a： 提供者](../../../ado/guide/appendixes/appendix-a-providers.md)。
