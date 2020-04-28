---
title: 附錄 G：回溯相容性的驅動程式方針 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292398"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>附錄 G：回溯相容性的驅動程式方針
本附錄提供在 ODBC 3 上運作之驅動程式寫入器的資訊。*x*驅動程式，需要支援 ODBC 2。*x*應用程式。 如需回溯相容性的詳細資訊，請參閱回溯[相容性和標準合規](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)性。  
  
 此章節包含下列主題。  
  
-   [Odbc 3.X 驅動程式的區塊資料指標、可滾動游標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)-新功能是存在於 odbc 3 的功能。*x* ，而不是 ODBC 2。*x*。 ODBC 3。*x*驅動程式通常不需要擔心與新功能的回溯相容性，因為 ODBC 2。*x*應用程式永遠不會使用它們。 唯一的例外狀況是與**SQLFetch**、 **SQLFetchScroll**、 **SQLSetPos**和**SQLExtendedFetch**相關的功能;如需詳細資訊，請參閱本附錄稍後的。  
  
-   [對應已取代](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)的函式-重複的功能是在 ODBC 3 中以不同方式執行的功能。*x*和 ODBC 2。*x*。 ODBC 3。*x*驅動程式不需要擔心與重複功能的回溯相容性，因為驅動程式管理員一律會對應 ODBC 2。*x*功能到 ODBC 3。*x*在呼叫 ODBC 3 時的功能。*x*驅動程式。 因此是 ODBC 3。*x*驅動程式只會看到 ODBC 3。*x*功能。 如需這些對應的詳細資訊，請參閱本附錄稍後的。  
  
-   行為[變更和 odbc 3.X 驅動程式](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md)-行為變更是在 ODBC 3 中以不同方式處理的功能。*x*和 ODBC 2。*x*。 ODBC 3。*x*驅動程式必須擔心行為變更，並採取行動以回應應用程式所設定的 SQL_ATTR_ODBC_VERSION 環境屬性。
