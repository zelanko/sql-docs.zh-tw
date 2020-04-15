---
title: 受影響的 ODBC 元件 |微軟文件
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
ms.openlocfilehash: 8d9155fa1c9df5846f069e93a3db1b969e9219ed
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306472"
---
# <a name="affected-odbc-components"></a>受影響的 ODBC 元件
向後相容性描述應用程式、驅動程式管理員和驅動程式如何受到新版本驅動程式管理器的影響。 當應用程式和驅動程式都保留在舊版本中時,這會影響它們。 因此,需要考慮三種類型的向後相容性,如下表所示。  
  
|類型|DM 版本|應用程式版本|驅動程式版本|  
|----------|-------------------|----------------------------|-----------------------|  
|驅動程式管理員的向後相容性|*3.x*|*2.x*|*2.x*|  
|驅動程式的向後相容性[1]|*3.x*|*2.x*|*3.x*|  
|應用程式向後相容性|*3.x*|*3.x*|*2.x*|  
  
 [1] 驅動程式的向後相容性主要在附錄 G:向後相容性驅動程式指南中討論。  
  
> [!NOTE]
>  符合標準的應用程式(例如,已按照開放組或 ISO CLI 標準編寫的應用程式)保證透過 ODBC *3.x*驅動程式管理員與 ODBC *3.x*驅動程式配合使用。 假定應用程式正在使用的功能在驅動程式中可用。 還假定符合標準的應用程式已使用 ODBC *3.x*標頭檔進行編譯。
