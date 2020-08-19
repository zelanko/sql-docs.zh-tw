---
description: 介面一致性層級
title: 介面一致性層級 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb77ab0e77fc8a811acd956673a4ad4fe8664828
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424620"
---
# <a name="interface-conformance-levels"></a>介面一致性層級
這項功能的目的是要通知應用程式可從驅動程式取得哪些功能。 以函式為基礎的「調節」配置無法達到這個目標。 在 ODBC 3 中。*x*，驅動程式會根據它們所擁有的功能進行分類。 支援此功能可能包括支援函式;它也可以包含支援描述項欄位、語句屬性、 **SQLGetInfo**所傳回之資訊類型的 "Y" 值等等。  
  
 為了簡化介面一致性的規格，ODBC 定義了三個一致性層級。 為了符合特定的一致性層級，驅動程式必須滿足該一致性層級的所有需求。 符合指定層級的與所有較低層級的完整一致性。  
  
 一致性層級不一定會整齊地細分為特定 ODBC 函數清單的支援，但請指定支援的功能，如下列各節所列。 若要提供功能的支援，驅動程式必須支援特定 ODBC 函數的部分或所有呼叫 (如需詳細資訊，請參閱函式 [一致性](../../../odbc/reference/develop-app/function-conformance.md)) 、設定某些屬性 (請參閱 [屬性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)) ，以及某些描述項欄位 (查看 [描述項欄位一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)) 。  
  
 應用程式會藉由連接到資料來源，並使用 SQL_ODBC_INTERFACE_CONFORMANCE 選項呼叫 **SQLGetInfo** ，來探索驅動程式的介面一致性層級。  
  
 驅動程式可自由地在其宣稱完全一致的層級以外的程度執行功能。 應用程式會藉由呼叫 **SQLGetFunctions** (來探索任何這類的額外功能，以判斷哪些 odbc 函數存在) 和 **SQLGetInfo** (來查詢不同) 的其他 odbc 功能。  
  
 有三個 ODBC 介面一致性層級：核心、層級1和層級2。  
  
> [!NOTE]
>  這些一致性層級的需求與 ODBC 2.x 中相同名稱的 ODBC API 一致性層級不同 *。* 尤其是，ODBC*2.X API 一致性* 層級1所隱含的所有功能現在都是核心介面一致性層級的一部分。 因此，許多 ODBC 驅動程式可能會報告核心層級介面一致性。  
  
 此章節包含下列主題。  
  
-   [核心介面一致性](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [層級 1 介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [函式一致性](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [屬性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [描述項欄位一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
