---
title: 一致性層級 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
- conformance levels [ODBC]
- conformance levels [ODBC], about conformance levels
ms.assetid: f776d467-5d5d-4761-9043-3dad5f73c610
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 17e11f8dd61de45f7ce046241695f3dcc901e254
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="conformance-levels"></a>一致性層級
ODBC 驅動程式可讓應用程式存取不同資料來源。 每個驅動程式可讓應用程式在執行階段決定哪些 ODBC 功能和哪些 SQL 文法的驅動程式，而且每個資料來源支援。 這不是設計來搭配單一驅動程式或一組小型、 已知的驅動程式，因為這些應用程式可以直接寫入該驅動程式或驅動程式的功能的應用程式的需求。 若要協助應用程式探索驅動程式和資料來源的功能，兩個區域的一致性是否可用： SQL 文法與 ODBC 介面。  
  
 此章節包含下列主題。  
  
-   [介面一致性層級](../../../odbc/reference/develop-app/interface-conformance-levels.md)  
  
-   [SQL 一致性層級](../../../odbc/reference/develop-app/sql-conformance-levels.md)
