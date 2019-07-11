---
title: 回溯相容性與標準相容性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], standards compliance
- compatibility [ODBC], standards compliance
- standards compliance [ODBC]
ms.assetid: b5eee7be-28ed-4467-8cf1-2205e2010a53
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc89fd8d43df4b906f47ab1ef6b6932a5a814a86
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794113"
---
# <a name="backward-compatibility-and-standards-compliance"></a>回溯相容性和標準合規性
回溯相容性是較新的 ODBC 元件能夠使用舊的 ODBC 元件。 下列各節將討論如何這些元件會受到在 ODBC 中的變更*3.x*。 主要是在其中所包含的資訊主要討論 ODBC 將寫入*3.x*應用程式，以及如何向後相容性問題會由 ODBC 驅動程式。 如何提供回溯相容性有關的特定指導方針的問題會影響撰寫 ODBC *3.x*驅動程式，請參閱[附錄 g:為了與舊版相容的驅動程式方針](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)。  
  
 此章節包含下列主題。  
  
-   [受影響的 ODBC 元件](../../../odbc/reference/develop-app/affected-odbc-components.md)  
  
-   [變更的類型](../../../odbc/reference/develop-app/types-of-changes.md)  
  
-   [應用程式/驅動程式相容性](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)  
  
-   [新增功能](../../../odbc/reference/develop-app/new-features.md)  
  
-   [重複的功能](../../../odbc/reference/develop-app/duplicated-features.md)  
  
-   [行為變更](../../../odbc/reference/develop-app/behavioral-changes.md)  
  
-   [撰寫 ODBC 3.x 應用程式](../../../odbc/reference/develop-app/writing-odbc-3-x-applications.md)  
  
-   [撰寫 ODBC 3.x 驅動程式](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)
