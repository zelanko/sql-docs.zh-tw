---
title: 關於 OLE DB 連線屬性 | Microsoft Docs
description: 關於 OLE DB 屬性
ms.custom: ''
ms.date: 05/20/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, properties
- OLE DB Driver for SQL Server, properties
- properties [OLE DB]
- property values [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: fa2fbb56d9d8926c45970ecddfabd226c87d26e2
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004449"
---
# <a name="about-ole-db-properties"></a>關於 OLE DB 屬性
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

<!--
NOTE , GeneMi , 2020/May/20:
    This SQL 2016+ article is a nearly exact duplicate of another SQL 2016+ article.
    This article resides under docs/connect/oledb/ole-db-driver/.

    The other article resides under docs/relational-databases/native-client-ole-db-provider/.
    And, the other article has a SQL 2014 counterpart having its same GitHub directory path and filename, to support SQL 2014 OPS Versioning with SQL 2016+.

    This path-file name is:
'\sql-docs-pr\docs\connect\oledb\ole-db-driver\about-ole-db-properties.md'.

    The other path-file is named:
'\sql-docs-pr\docs\relational-databases\native-client-ole-db-provider\about-ole-db-properties.md'.

    Therefore, maybe this docs/connect/oledb/... file should be deleted?

1611957:  This NOTE relates to SEO content bug 1611957 about metadata 'title:' value duplication:
    https://mseng.visualstudio.com/TechnicalContent/_workitems/edit/1611957

PR 15068:  This HTML comment is being added by PR...
    https://github.com/MicrosoftDocs/sql-docs-pr/pull/15068
-->

  取用者會設定屬性值來要求特定的物件行為。 例如，取用者會使用屬性來指定要由某個資料列集公開的介面。 取用者會取得屬性值來判斷物件 (例如資料列集、工作階段或資料來源物件) 的功能。  
  
 每個屬性 (Property) 都有一個值、類型、描述和讀取/寫入屬性 (Attribute)，而且資料列集屬性 (Property) 還會包含一個指標，表示它是否能夠以逐資料行的方式套用。  
  
 屬性是由 GUID 以及代表屬性識別碼的整數所識別。 屬性集是共用相同 GUID 之所有屬性的集合。 除了預先定義的 OLE DB 屬性集以外，OLE DB Driver for SQL Server 會實作提供者特定的屬性集和其中的屬性。 每個屬性都屬於一或多個屬性群組。 屬性群組是套用至特定物件之所有屬性的群組。 某些屬性群組包括初始化屬性群組、資料來源屬性群組、工作階段屬性群組、資料列集屬性群組、資料表屬性群組和資料行屬性群組。 其中每個屬性群組都具有屬性。  
  
 設定屬性值包括：  
  
1.  決定要設定值的屬性。  
  
2.  決定包含已識別之屬性的屬性集。  
  
3.  配置 DBPROPSET 結構的陣列 (針對每個已識別的屬性集配置一個結構)。  
  
4.  針對每個屬性集配置 DBPROP 結構的陣列。 每個陣列中的元素數目就是屬於該屬性集的屬性數目 (在步驟 1 中識別)。  
  
5.  填入每個屬性的 DBPROP 結構。  
  
6.  填入每個屬性集之 DBPROPSET 結構的資訊 (屬性集 GUID、元素數目計數，以及指向對應 DBPROP 陣列的指標)。  
  
7.  呼叫方法來設定屬性並且傳遞 DBPROPSET 結構的計數和陣列。  
  
## <a name="see-also"></a>另請參閱  
 [建立 OLE DB Driver for SQL Server 應用程式](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [屬性 (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=112207)  
  
  
