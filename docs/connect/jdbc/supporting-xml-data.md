---
title: 支援 XML 資料 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 32b7217e-1f0c-473d-9a45-176daa81584e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 799b22cfac669846c606456f1911e27353a9ba9f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027708"
---
# <a name="supporting-xml-data"></a>支援 XML 資料
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供的 **xml** 資料類型，可讓您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中儲存 XML 文件和片段。 **xml** 資料類型是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的內建資料類型，而且在某些狀況下類似於其他內建類型，例如 **int** 和 **varchar**。 如同其他內建類型，您可以將 **xml** 資料類型當作變數類型、參數類型或函式傳回的類型使用；當作建立資料表時的資料行類型；或者在 [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 和 CONVERT 函式中使用。 在 JDBC 驅動程式中，**xml** 資料類型可以對應為字串、位元組陣列、資料流、CLOB、BLOB 或 SQLXML 物件。 字串為預設對應。  
  
 JDBC 驅動程式提供 JDBC 4.0 API 的支援，此 API 引進 SQLXML 介面。 SQLXML 介面會定義與 XML 資料互動和進行操作的方法。 **SQLXML** 是 JDBC 4.0 資料類型，而且其會對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**xml** 資料類型。 因此，若要在應用程式中使用 SQLXML 資料類型，您必須將 Classpath 設定為包含 sqljdbc4.jar 檔案。 如果應用程式在存取 SQLXML 物件及其方法時嘗試使用 sqljdbc3.jar，就會擲回例外狀況。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一定會先驗證 XML 資料，然後再將它儲存於資料庫資料行中。 應用程式可以使用 **SQLXML** 資料類型，因為 JDBC 驅動程式會自動將它對應至 **xml** 資料類型。 sqljdbc4.jar 提供 **SQLXML** 支援。 如需 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 所支援的 JRE 版本清單，請參閱 [JDBC 驅動程式的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
 本節中的主題描述 SQLXML 介面以及如何使用 JDBC API 方法來針對 **SQLXML** 資料類型進行程式設計。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[SQLXML 介面](../../connect/jdbc/sqlxml-interface.md)|描述 SQLXML 介面及其方法。|  
|[使用 SQLXML 進行程式設計](../../connect/jdbc/programming-with-sqlxml.md)|描述如何使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] API 方法，以便在關聯式資料庫中儲存及擷取 **SQLXML** Java 資料類型的 XML 資料。 同時包含有關 SQLXML 物件類型的資訊，並提供使用 SQLXML 物件時重要指導方針和限制的清單。|  
  
## <a name="see-also"></a>另請參閱  
 [了解 JDBC 驅動程式資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
