---
title: "SQLAllocConnect （Visual FoxPro ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAllocConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 70d48b12-def5-475c-b8e1-654a55fdfe0f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5614b69fddd5b5430f15e8266bef6872d4294f4e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallocconnect-visual-foxpro-odbc-driver"></a>SQLAllocConnect （Visual FoxPro ODBC 驅動程式）
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援： 完整  
  
 ODBC 應用程式開發介面相容性： 核心層級  
  
 將記憶體配置連接控制代碼給*hdbc*，識別在環境內*henv*。 驅動程式管理員會處理此呼叫，並呼叫驅動程式的**SQLAllocConnect**每當[SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)， **SQLBrowseConnect**，或[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)呼叫。  
  
 如需詳細資訊，請參閱[SQLAllocConnect](../../odbc/reference/syntax/sqlallocconnect-function.md)中*ODBC 程式設計人員參考*。

