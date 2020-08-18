---
description: 附錄 A：資料和服務提供者
title: 附錄 A：提供者 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- providers [ADO]
- ADO, providers
- service providers [ADO]
- service components [ADO]
ms.assetid: e2581b47-b11e-4e1e-b96c-d39c77c5b48a
author: rothja
ms.author: jroth
ms.openlocfilehash: d14a3399eb771965d039126ebf3672a8ad3d5190
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88396404"
---
# <a name="appendix-a-data-and-service-providers"></a>附錄 A：資料和服務提供者
本節將討論三種提供者：資料提供者、服務提供者和服務元件。 提供者分為兩種類別：提供資料的資料，以及提供服務的資料。 *資料提供者*擁有本身的資料，並以表格形式以表格形式公開給您的應用程式。 *服務提供者*會藉由產生和取用資料來封裝服務，以增強 ADO 應用程式中的功能。 服務提供者也可以進一步定義為 *服務元件*，該元件必須與其他服務提供者或元件一起使用。

## <a name="data-providers"></a>資料提供者
 ADO 的功能強大且有彈性，因為它可以連接到數個不同的資料提供者，而且仍會公開相同的程式設計模型，而不論任何指定的提供者有哪些特定功能。

 不過，因為每個資料提供者都是唯一的，所以您的應用程式與 ADO 互動的方式會因數據提供者而稍微不同。 差異通常屬於下列三種類別的其中一種：

-   [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性中的連接參數。

-   [命令](../../../ado/reference/ado-api/command-object-ado.md) 物件使用方式。

-   提供者特定的 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 行為。

 Microsoft 目前提供的每個資料提供者的詳細資料如下所示。

|區域|主題|
|----------|-----------|
|ODBC 資料庫|[Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Microsoft 索引服務|[Microsoft OLE DB Provider for Microsoft Indexing Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Active Directory 服務|[Microsoft OLE DB Provider for Microsoft Active Directory Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Microsoft Jet 資料庫|[適用于 Microsoft Jet 的 OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|Oracle 資料庫|[Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|網際網路發佈|[適用于網際網路發佈的 Microsoft OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|簡單資料來源|[Microsoft OLE DB 簡單提供者](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>提供者特定的動態屬性
 [連接](../../../ado/reference/ado-api/connection-object-ado.md)、[命令](../../../ado/reference/ado-api/command-object-ado.md)和[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合包含提供者特定的動態屬性。 這些屬性會提供提供者專屬功能的相關資訊，而這些資訊超出 ADO 所支援的內建屬性。

 建立連接並建立這些物件之後，請在物件的**Properties**集合上使用[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法，以取得提供者特定的屬性。 如需這些動態屬性的詳細資訊，請參閱提供者檔和《 OLE DB 程式設計 [人員指南》](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) 。

## <a name="service-providers"></a>服務提供者
 若要使用服務提供者，您必須提供關鍵字。 您也應該留意與每個服務提供者相關聯的提供者特定動態屬性。 針對 Microsoft 目前提供的每個服務提供者，列出提供者特定的詳細資料：

-   [Microsoft Data Shaping Service for OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Microsoft OLE DB 持續性提供者](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Microsoft OLE DB 遠端處理提供者](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>服務元件
 OLE DB 服務元件的資料 [指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 會補充資料提供者的資料指標支援功能。 它也需要關鍵字並且具有動態屬性。

 如需有關 OLE DB 提供者的詳細資訊，請參閱 [Microsoft OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)。

## <a name="provider-commands"></a>提供者命令
 針對此處所列的每個提供者，如果您的應用程式允許使用者輸入 SQL 語句作為提供者命令，您必須一律驗證使用者輸入，並使用可能有危險的 SQL 語句（例如 `DROP TABLE t1` ）做為使用者輸入的一部分，以避免駭客攻擊。

## <a name="see-also"></a>另請參閱
 [命令物件 (ado) ](../../../ado/reference/ado-api/command-object-ado.md) [CONNECTION 物件 (ado) ](../../../ado/reference/ado-api/connection-object-ado.md) [Microsoft OLE DB provider for Internet 發行](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)Microsoft OLE DB provider for microsoft Active Directory [Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [microsoft OLE DB](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)提供者 for microsoft OLE DB Service microsoft Microsoft OLE DB Provider for Oracle 提供[者 OLE DB](../../../ado/reference/ado-api/recordset-object-ado.md) [SQL Server OLE DB (](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)) [的](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) ([提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [Properties Collection (ADO) ](../../../ado/reference/ado-api/properties-collection-ado.md) [)  () ](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) [的](../../../ado/reference/rds-api/refresh-method-rds.md)
