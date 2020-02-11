---
title: 受影響的 ODBC 元件 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 08997f610b00f22d436a5c91d34beb2a8fc2cc1d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67944858"
---
# <a name="affected-odbc-components"></a>受影響的 ODBC 元件
回溯相容性說明新版本驅動程式管理員的引進，如何影響應用程式、驅動程式管理員和驅動程式。 這會影響應用程式和驅動程式，而兩者的其中一個或兩個都保留在舊版本中。 因此，有三種類型的回溯相容性需要考慮，如下表所示。  
  
|類型|DM 的版本|應用程式版本|驅動程式版本|  
|----------|-------------------|----------------------------|-----------------------|  
|驅動程式管理員的回溯相容性|*3.x*|*2.x*|*2.x*|  
|驅動程式的回溯相容性 [1]|*3.x*|*2.x*|*3.x*|  
|應用程式的回溯相容性|*3.x*|*3.x*|*2.x*|  
  
 [1] 驅動程式的回溯相容性主要在附錄 G：驅動程式方針中討論回溯相容性。  
  
> [!NOTE]
>  符合標準的應用程式（例如，根據開放式群組或 ISO CLI 標準撰寫的應用程式）保證會*透過 odbc 3.X* *驅動程式管理員與 odbc 3.x*驅動程式搭配使用。 它會假設應用程式使用的功能在驅動程式中提供。 同時也假設符合標準的應用程式已*使用 ODBC 3.x*標頭檔進行編譯。
