---
description: 受影響的 ODBC 元件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4874a22d441ec856c25e08dc20cf04e0f0be89cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424860"
---
# <a name="affected-odbc-components"></a>受影響的 ODBC 元件
回溯相容性描述應用程式、驅動程式管理員和驅動程式如何隨著新版本的驅動程式管理員而受到影響。 這會影響應用程式和驅動程式，因為兩者或兩者都維持在舊版本中。 因此，您可以考慮三種回溯相容性，如下表所示。  
  
|類型|DM 的版本|應用程式的版本|驅動程式版本|  
|----------|-------------------|----------------------------|-----------------------|  
|驅動程式管理員的回溯相容性|*3.x*|*2.x*|*2.x*|  
|驅動程式的回溯相容性 [1]|*3.x*|*2.x*|*3.x*|  
|應用程式的回溯相容性|*3.x*|*3.x*|*2.x*|  
  
 [1] 驅動程式的回溯相容性主要是在附錄 G：適用于回溯相容性的驅動程式指導方針中討論。  
  
> [!NOTE]
>  符合標準的應用程式（例如，根據 Open Group 或 ISO CLI 標準所撰寫的應用程式），保證可*透過 odbc 3.X 驅動程式管理員**使用 odbc 3.x 驅動程式。* 假設應用程式使用的功能可在驅動程式中使用。 也假設符合標準的應用程式已 *使用 ODBC 3.x* 標頭檔編譯。
