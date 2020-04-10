---
title: 使用 JDBC 驅動程式處理中繼資料 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5cfb35d4-ddcd-40a2-8091-f29cddc32552
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 859932404e14a9ab1216665d211e1b6734ca9726
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924682"
---
# <a name="handling-metadata-with-the-jdbc-driver"></a>使用 JDBC 驅動程式處理中繼資料
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 可用許多不同方式來處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的中繼資料。 JDBC 驅動程式可用來取得有關資料庫的中繼資料、結果集或參數。  
  
 JDBC 驅動程式提供三種類別來擷取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的中繼資料：  
  
-   [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)，用來傳回目前所連線資料庫的相關資訊。  
  
-   [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)，用來傳回結果集的相關資訊。  
  
-   [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md)，用來傳回已準備和可呼叫陳述式的參數相關資訊。  
  
 本節中的主題描述如何使用這三個中繼資料類型來使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的中繼資料。  
  
> [!NOTE]  
>  從應用程式效能方面來看，本節所討論的中繼資料方法一般而言成本較高，因此使用時要小心。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[使用資料庫中繼資料](../../connect/jdbc/using-database-metadata.md)|描述如何擷取有關目前連接之資料庫的中繼資料資訊。|  
|[使用結果集中繼資料](../../connect/jdbc/using-result-set-metadata.md)|描述如何擷取有關目前結果集的中繼資料資訊。|  
|[使用參數中繼資料](../../connect/jdbc/using-parameter-metadata.md)|描述如何擷取已準備和可呼叫陳述式的參數相關資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
