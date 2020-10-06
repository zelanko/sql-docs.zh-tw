---
description: 服務提供者和元件
title: 服務提供者和元件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
author: rothja
ms.author: jroth
ms.openlocfilehash: 0f0c89d8a7f83bebfa77fb02a282fc21cb6f2dd0
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724939"
---
# <a name="service-providers-and-components"></a>服務提供者和元件
服務提供者是一種元件，可透過執行資料存放區原生不支援的延伸介面，來擴充資料提供者的功能。  
  
 通用資料存取提供的 *元件架構* 可讓個別、特製化的元件在功能較少的存放區上，執行一組離散的資料庫功能或「服務」。 因此，不需要強制每個資料存放區提供自己的擴充功能，或強制一般應用程式在內部執行資料庫功能，服務元件會提供任何應用程式在存取任何資料存放區時可使用的常見實作為。 有些功能是由資料存放區以原生方式執行，有些則是透過泛型元件，對應用程式而言是透明的。  
  
 例如，資料指標引擎（例如 [OLE DB 的資料指標服務](/previous-versions/windows/desktop/ms714397(v=vs.85))）是一種服務元件，它可以取用連續、順向資料存放區的資料，以產生可滾動的資料。 ADO 常用的其他服務提供者包括 [microsoft OLE DB 持續性提供者 (ADO 服務提供者) ](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) (將資料儲存至檔案) 、適用于 [OLE DB (Ado 服務提供者的 Microsoft 資料成形服務 ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md))  () 的階層式 **記錄集** OLE DB，以及 [MICROSOFT (遠端處理提供者) ado 服務提供 ](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) 商 () ，以在遠端電腦上叫用資料提供者。  
  
 如需服務和資料提供者的詳細資訊，請參閱 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)。