---
title: 類型的變更 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ac92c6d40ea9ead6b8875e3338bb740b4bdf8523
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473180"
---
# <a name="types-of-changes"></a>變更的類型
ODBC 3 進行三種類型的變更。*x* （和 ODBC 的任何版本）。 每一種方式會影響回溯相容性，並以不同方式處理。 下表說明這些變更。  
  
|變更類型|描述|  
|--------------------|-----------------|  
|新增功能|這些是 ODBC 3 不熟悉的功能。*x*，例如程式碼外部繫結或描述元。 只有在應用程式和驅動程式，以及驅動程式管理員 中，屬於第 3 版時，這些會實 *.x*，這樣就不會嘗試讓這些具有回溯相容性。|  
|重複的功能|這些是存在於 ODBC 2 的功能 *.x*而 ODBC 3。*x* ，但會在每個不同的方式實作。 函式**SQLAllocHandle**並**SQLAllocStmt**即為一例。 回溯相容性問題的這些和其他重複的功能大部分都由驅動程式管理員中的對應。|  
|行為變更|這些是 ODBC 2 中以不同方式處理的功能 *.x*而 ODBC 3。*x*。 日期時間 **#define**是範例。 這些功能是由 ODBC 3 處理。*x*驅動程式為基礎的環境屬性設定。 (請參閱[的行為變更](../../../odbc/reference/develop-app/behavioral-changes.md)如需詳細資訊。)|
