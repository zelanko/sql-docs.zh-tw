---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4ffecfc87ec23fc4d62174dae31220511c9f72d4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926974"
---
# <a name="appendix-a-data-and-service-providers"></a>附錄 A：資料和服務提供者
本節說明三種提供者：資料提供者、服務提供者和服務元件。 提供者分成兩個類別：提供資料和提供服務的人員。 *資料提供者*擁有自己的資料，並以表格式形式將它公開給您的應用程式。 *服務提供者*會藉由產生和取用資料，在您的 ADO 應用程式中擴充功能來封裝服務。 服務提供者也可以進一步定義為*服務元件*，這必須與其他服務提供者或元件搭配使用。

## <a name="data-providers"></a>資料提供者
 ADO 的功能強大且有彈性，因為它可以連接到數種不同的資料提供者，而且仍然會公開相同的程式設計模型，不論任何指定的提供者的特定功能為何。

 不過，因為每個資料提供者都是唯一的，所以您的應用程式與 ADO 互動的方式會因數據提供者而稍微不同。 這些差異通常屬於下列三種類別的其中一種：

-   [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性中的連接參數。

-   [命令](../../../ado/reference/ado-api/command-object-ado.md)物件使用方式。

-   提供者特定的[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)行為。

 目前可從 Microsoft 取得的每個資料提供者的詳細資訊如下所示。

|區域|主題|
|----------|-----------|
|ODBC 資料庫|[Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Microsoft 索引服務|[Microsoft OLE DB Provider for Microsoft Indexing Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Active Directory 服務|[Microsoft OLE DB Provider for Microsoft Active Directory 服務](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Microsoft Jet 資料庫|[適用于 Microsoft Jet 的 OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|Oracle 資料庫|[Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|網際網路發佈|[適用于網際網路發佈的 Microsoft OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|簡單資料來源|[Microsoft OLE DB 簡單提供者](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>提供者特定的動態屬性
 [Connection](../../../ado/reference/ado-api/connection-object-ado.md)、 [Command](../../../ado/reference/ado-api/command-object-ado.md)和[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)物件的[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合包含提供者特定的動態屬性。 這些屬性會提供提供者特定功能的相關資訊，而不限於 ADO 支援的內建屬性。

 建立連接並建立這些物件之後，請在物件的**Properties**集合上使用[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法，以取得提供者特定的屬性。 如需這些動態屬性的詳細資訊，請參閱提供者檔和 OLE DB 程式設計[人員指南](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)。

## <a name="service-providers"></a>服務提供者
 若要使用服務提供者，您必須提供關鍵字。 您也應該注意與每個服務提供者相關聯的提供者特定動態屬性。 系統會針對目前可從 Microsoft 取得的每個服務提供者，列出提供者特定的詳細資料：

-   [Microsoft Data Shaping Service for OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Microsoft OLE DB 持續性提供者](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Microsoft OLE DB 遠端處理提供者](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>服務元件
 OLE DB 服務元件的[Cursor 服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)會補充資料提供者的資料指標支援函數。 它也需要關鍵字，而且具有動態屬性。

 如需有關 OLE DB 提供者的詳細資訊，請參閱[Microsoft OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)。

## <a name="provider-commands"></a>提供者命令
 針對此處所列的每個提供者，如果您的應用程式允許使用者輸入 SQL 語句做為提供者命令，您必須一律驗證使用者輸入，並使用可能危險的 SQL 語句（例如`DROP TABLE t1`）做為使用者輸入的一部分，以預防可能的駭客攻擊。

## <a name="see-also"></a>另請參閱
 [Command 物件（ado）](../../../ado/reference/ado-api/command-object-ado.md) [連線物件（ado）](../../../ado/reference/ado-api/connection-object-ado.md) [Microsoft OLE DB provider For Internet 發行](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) [microsoft OLE DB Provider for microsoft Active Directory Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [Microsoft OLE DB PROVIDER for microsoft 索引服務 microsoft](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md) [OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) [Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) [MICROSOFT OLE DB provider](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) for [microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [Properties Collection （ado）](../../../ado/reference/ado-api/properties-collection-ado.md) [記錄集物件（ado](../../../ado/reference/ado-api/recordset-object-ado.md) ） [Refresh 方法（RDS）](../../../ado/reference/rds-api/refresh-method-rds.md)
