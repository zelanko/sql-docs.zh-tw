---
title: "取得描述項處理 |Microsoft 文件"
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
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eb3d75a78a5eaa516921e561cb2d34786804d182
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="obtaining-descriptor-handles"></a>取得描述項處理
應用程式當做輸出引數的呼叫中取得的任何明確配置描述項控制代碼**SQLAllocHandle**。 隱含地配置描述項的控制代碼透過呼叫**SQLGetStmtAttr**。
