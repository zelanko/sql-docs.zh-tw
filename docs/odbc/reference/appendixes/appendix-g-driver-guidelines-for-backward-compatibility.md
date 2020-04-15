---
title: 附錄 G:向後相容性的驅動程式指南 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 911cd335-f2c0-4d03-9739-1078308a678a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1055f94cb54bba9262f210e5df5f028029aebf5b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292398"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>附錄 G：回溯相容性的驅動程式方針
本附錄為在 ODBC 3 上工作的驅動程式編寫者提供資訊。*x*需要支援 ODBC 2 的驅動程式。*x*應用程式。 有關向後相容性的詳細資訊,請參閱[向後相容性和標準合規性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 此章節包含下列主題。  
  
-   [塊游標、可滾動游標和向後相容性的 ODBC 3.x 驅動程式](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)- 新功能是 ODBC 3 中存在的功能。*x,* 而不是ODBC 2。*x*. . ODBC 3.*x*驅動程式通常不必擔心與新功能的向後相容性,因為ODBC 2。*x*應用程式從不使用它們。 唯一的例外是與**SQLSetPos**SQLFetch、SQLFetchScroll、SQLSetPos 和 SQL**擴展獲取**相關的功能。 **SQLFetch** **SQLFetchScroll**有關詳細資訊,請參閱 本附錄後面的 。。  
  
-   [映射棄用函數](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)- 重複功能是在 ODBC 3 中以不同的方式實現的功能。*x*和 ODBC 2。*x*. . ODBC 3.*x*驅動程式不必擔心與重複的要素的向後相容性,因為驅動程式管理器始終映射 ODBC 2。*x* ODBC 3 的功能。*x*呼叫 ODBC 3 時的功能。*x*驅動程式。 因此,ODBC 3。*x*驅動程式只能看到 ODBC 3。*x*功能。 有關這些映射的詳細資訊,請參閱 本附錄後面的 。  
  
-   [行為更改和 ODBC 3.x 驅動程式](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md)- 行為更改是在 ODBC 3 中以不同的方式處理的功能。*x*和 ODBC 2。*x*. . ODBC 3.*x*驅動程式必須擔心行為更改,並回應應用程式設置SQL_ATTR_ODBC_VERSION環境屬性。
