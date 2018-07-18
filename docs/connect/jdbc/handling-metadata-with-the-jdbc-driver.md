---
title: 處理中繼資料，JDBC 驅動程式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5cfb35d4-ddcd-40a2-8091-f29cddc32552
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b6fbf435775709ec9890b1c26832b1730f8c6d31
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32829413"
---
# <a name="handling-metadata-with-the-jdbc-driver"></a>使用 JDBC Driver 處理中繼資料
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]可以用來處理中繼資料中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫中有許多種。 JDBC 驅動程式可用來取得有關資料庫的中繼資料、結果集或參數。  
  
 JDBC 驅動程式提供三種類別來擷取中繼資料從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫：  
  
-   [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)，用來傳回目前連接之資料庫的相關資訊。  
  
-   [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)，用來傳回結果集的相關資訊。  
  
-   [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md)，用來傳回已備妥及可呼叫陳述式的參數資訊。  
  
 本節主題說明如何使用三個中繼資料類別的每個使用中的中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。  
  
> [!NOTE]  
>  從應用程式效能方面來看，本節所討論的中繼資料方法一般而言成本較高，因此使用時要小心。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[使用資料庫中繼資料](../../connect/jdbc/using-database-metadata.md)|描述如何擷取有關目前連接之資料庫的中繼資料資訊。|  
|[使用結果集中繼資料](../../connect/jdbc/using-result-set-metadata.md)|描述如何擷取有關目前結果集的中繼資料資訊。|  
|[使用參數中繼資料](../../connect/jdbc/using-parameter-metadata.md)|描述如何擷取已準備和可呼叫陳述式的參數相關資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
