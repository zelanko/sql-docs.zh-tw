---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5f43dbf75754a16b3163bbb8e268400f34d372b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087811"
---
# <a name="types-of-changes"></a>變更的類型
ODBC 3.x （和任何版本*的 odbc）* 中會進行三種類型的變更。 其中每個都會影響回溯相容性，並以不同的方式處理。 下表將說明這些變更。  
  
|變更類型|描述|  
|--------------------|-----------------|  
|新功能|這些*是 ODBC 3.x*的新功能，例如非正規系結或描述元。 只有當應用程式和驅動程式，以及驅動程式*管理員版本為*3.x 時，才會執行這些動作，因此不會嘗試讓這些回溯相容。|  
|重複的功能|這些是存在*于 odbc* 2.X 和 odbc 3.x 中的*功能，但*在每個中都是以不同的方式來執行。 **SQLAllocHandle**和**SQLAllocStmt**函式是一個範例。 這些和其他重複功能的回溯相容性問題大部分都是由驅動程式管理員中的對應來處理。|  
|行為變更|這些是在 ODBC *2.x 和 odbc* 3.x 中以不同方式處理的*功能。* 日期時間 **#define**是一個範例。 這些功能是*由 ODBC 3.x*驅動程式根據環境屬性設定來處理。 （如需詳細資訊，請參閱[行為變更](../../../odbc/reference/develop-app/behavioral-changes.md)）。|
