---
description: 資料指標程式庫作業
title: 資料指標程式庫作業 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], backward compatibility
- compatibility [ODBC], cursor library
- upgrading applications [ODBC], cursor library
- application upgrades [ODBC], cursor library
- backward compatibility [ODBC], cursor library
- cursor library [ODBC], backward compatibility
ms.assetid: 04d514b1-dc4d-4b84-bf35-60f4657ef1f6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: efe3191e264fe45307ef90624f6b6e76d4ccaff6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429410"
---
# <a name="cursor-library-operations"></a>資料指標程式庫作業
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 如果使用 ODBC 2.x 驅動程式的應用程式*呼叫 odbc 3.x* *資料指標連結*庫，應用程式可能可以使用 odbc 2.x 驅動程式不支援*的*odbc *3.x 功能。* 但是，應用程式撰寫者應該小心使用這些功能。 使用 ODBC 3.x 資料*指標連結*庫並不會將 odbc 2.x 驅動程式設*為 odbc 3.x* *驅動程式。*
