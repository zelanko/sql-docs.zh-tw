---
description: 變更的類型
title: 變更的類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46866c49a36711a8072895deb816a9d9110f5035
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476302"
---
# <a name="types-of-changes"></a>變更的類型
有三種類型的變更是在 ODBC 3.x (和任何版本 *的 odbc) * 中進行。 其中每個都會影響回溯相容性，並以不同的方式處理。 下表將說明這些變更。  
  
|變更的類型|描述|  
|--------------------|-----------------|  
|新功能|這些 *是 ODBC 3.x*的新功能，例如非正規系結或描述項。 只有當應用程式和驅動程式，以及驅動程式管理員是 *3.x 版時*，才會執行這些功能，因此不會嘗試讓這些版本回溯相容。|  
|重複的功能|這些是存在*于 odbc* 2.X 和 odbc 3.x 中的*功能，但*各有不同的執行方式。 **SQLAllocHandle**和**SQLAllocStmt**函式都是範例。 這些和其他重複功能的回溯相容性問題大部分都是由驅動程式管理員中的對應來處理。|  
|行為變更|這些是 ODBC *2.x 和 odbc* 3.x 中以不同方式處理的功能 *。* Datetime **#define** 為範例。 這些功能是 *由 ODBC 3.x* 驅動程式根據環境屬性設定來處理。  (如需詳細資訊，請參閱 [行為變更](../../../odbc/reference/develop-app/behavioral-changes.md) 。 ) |
